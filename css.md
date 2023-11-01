# Flexbox with text ellipsis

### key recipes:  
- Set `min-width: 0;` in the flex container
- Set `flex-shrink: 0;` in the flex-child to prevent an ellipsis from showing.

 
```html
<div class="filename">
  <span class="filename__base">this-file-has-a-really-really-really-long-filename.</span>
  <span class="filename__extension">pdf</span>
</div>
```
and
```css
.filename {
  display: flex;
  min-width: 0;
}

.filename__base {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

.filename__extension {
  flex-shrink: 0;
}
```

## Reference
1. [CSS-Tricks: Using Flexbox and text ellipsis together](https://css-tricks.com/using-flexbox-and-text-ellipsis-together/)
