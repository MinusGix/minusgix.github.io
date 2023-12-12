# Tips & Tricks

## Out of Range Colors
Sometimes you want to debug your out of range colors, but you can't really easily visualize them. If there's a long region of pure black, is that due to accidentally going negative or is it just outputting `0`?  
One hacky way to debug this is to set the color values to `fract(x)`, (which is just `x - floor(x)`).  
This would mean that if it was `2.4` then it would output `0.4`, etc. So if you went over notably, you'd see it repeat.