<script>
    import {onMount} from 'svelte'

    export let rowHeight = 0;
    export let data = [];
    export let visibleRows = 0;
    let visibleData = data.slice(0, visibleRows);
    let virtualBottom = (data.length - visibleRows) * rowHeight;
    let virtualTop = 0; 
    let virtualContainerRef;
    onMount(()=>{
        if(virtualContainerRef)
            virtualContainerRef?.addEventListener('scroll', onScrolling)
    })
    const onScrolling = () => {
        if(virtualContainerRef.scrollTop < (data.length)*rowHeight){
            let scrollTop = virtualContainerRef.scrollTop;
            let topIndex = Math.floor(scrollTop / rowHeight);
            let lastIndex = Math.min(topIndex + visibleRows, data.length+1)
            let newVirtualTop = Math.max( rowHeight * topIndex, 0);
            let newVirtualBottom = Math.max((data.length - visibleRows - topIndex) * rowHeight, 0);
            if(newVirtualTop !== virtualTop){
                visibleData = data.slice(topIndex, lastIndex)
                virtualTop = newVirtualTop
                virtualBottom = newVirtualBottom;
            }
        }
    }

</script>

<div class='virtual-container' bind:this={virtualContainerRef}>
    <div id='virtual-top' style="height: {virtualTop}px"></div>
    <div class='main-scroll' on:scroll={onScrolling}>
        {#each visibleData as row, i}
            <slot item={row}></slot>
        {/each}
    </div>
    <div id='virtual-bottom' style="height: {virtualBottom}px"></div>
</div>


<style>
    .virtual-container{
        overflow-anchor: none;
        height: 100%;
        width: 100%;
        overflow: auto;
    }
</style>