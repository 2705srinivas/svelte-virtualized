# svelte-scroll-infinite-list

Use this package to lazy-load a list based on pagination. It improves performance for large lists by rendering given no. of rows at a time.

### Installation 🔧



```bash
yarn add svelte-scroll-infinite-list
``` 

or

```bash
npm install svelte-scroll-infinite-list
``` 


### Usage ⌨️

_Explain what these tests verify and why_

```html
<script>
    import VirtualScroll from 'svelte-scroll-infinite-list';
    const data = new Array(100).fill(10);
</script>

<div style='height: 300px; width: 300px; border: 1px solid black;'>
   <VirtualScroll 
     data={data}
     rowHeight={18} 
     visibleRows={30} 
     let:item >
        <div>{item}</div>
   </VirtualScroll>
</div>
```

1. `scroll container dimensions or other styles` ---
For specifying height and width of the scroll container, wrap the `VirtualScroll` element with a `div` by giving height and width as show in example above. Other styles also can be specified like border in the example above.

2. `data`(mandatory) --- Array of data that list has to render.
3. `rowHeight`(mandatory) --- Height of each row in the list.
4. `visibleRows`(mandatory) --- Number of rows at max to render in the list. Usually based on the view height of a screen, a number to be specified.

⌨️ with ❤️ by [Srinivas] 😊