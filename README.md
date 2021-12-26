# tiny-mandelbrot

A variable resolution Mandelbrot visualizer for the JS canvas in **just 244 bytes**

![mandelbrot resulting image](mandelbrot.png)

Try it yourself! https://missing-user.github.io/tiny-mandelbrot/

And here's another version using modulo 4 for high contrast coloring:
https://missing-user.github.io/tiny-mandelbrot/pretty_high_contrast

## Code

- **219 bytes** minified at a fixed resolution of 1000x1000px:

  ```html
  <body
  onload=for(c=a.getContext`2d`,a.height=a.width=h=1e3,M=c.createImageData(h,h),k=x=h*h;x--;M.data[4*x-1]=i)for(i=I=R=0;i<255&I*I+R*R<2;i++)T=I*R,I=I*I-R*R-2+x%h/h*4,R=2*T-2+4*x/k;c.putImageData(M,0,0)><canvas
    id="a"
  >
  ```

- **244 bytes** version with resolution query string support (Change the Query String at the end of the URL, to load a different the resolution, e.g. https://missing-user.github.io/tiny-mandelbrot#1500 for 1500x1500px):

  ```html
  <body onload=for(c=a.getContext`2d`,a.height=a.width=h=location.hash.substr(1)||1e3,M=c.createImageData(h,h),k=x=h*h;x--;M.data[4*x-1]=i)for(i=I=R=0;i<255&I<2&R<2;i++)T=I*R,I=I*I-R*R-2+x%h/h*4,R=2*T-2+4*x/k;c.putImageData(M,0,0)><canvas id=a>
  ```

## Minification

- The first thing that one might notice is that there is no `<html>` or `<head>` wrapping the code, since both will be inserted by the browser automatically and therefore aren't required. The body is also missing the closing tag, since the HTML spec will correct this mistake and it saves us 7 more bytes.

- To add JavaScript into HTML I use the body onload function, saving 5 bytes over `<script></script>` tags.

- Because the code is written as a continuous string, we can omit the parentheses around the argument of the onload function, saving 2 bytes. `onload="..."` -> `onload=...`.

- Chained assignments are being used whenever possible to save a few characters like so:
  `i=0; j=0; w=0` can be reduced to `i=j=w=0`

- The exit condition for the loop was `i<255 && Math.sqrt(zi*zi + zr*zr)<2` which was first reduced to `i<255 && zi*zi + zr*zr<4` and then to `i<255&zi<2&zr<2` for the final version. The single & symbols are bitwise operators, which in this instance have the same effect as the and operator (&&)

- The brackets around the for loop can be removed:
  `for(...){foo(); bar();}` by chaining the methods with commas like so `for(...) foo(), bar()`

- Instead of saving the image data to a separate variable, directly access it, since it only appears once in the code.
  `data = img.data; data[i*4]=1` turns into `img.data[i*4]=1`

- Just setting the alpha channel of the image data instead of all channels, this way the color defaults to black and we save building a for loop to iterate through the colors. I know that the drawing code could be made smaller by using `ctx.fillRect()` instead, but then the page takes several seconds to load, which is inacceptable in my oppinion.
