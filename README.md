# tiny-mandelbrot

A Mandelbrot visualizer for the JS canvas in under 1kb.

Check it out [here](https://missing-user.github.io/tiny-mandelbrot)

The full code:
``<canvas id=a><script>for(c=a.getContext`2d`,a.height=a.width=h=1e3,g=c.createImageData(h,h),m=g.data,o=3,y=h;y--;)for(x=h;x--;m[o+=4]=i)for(i=j=k=0;i<255&j*j+k*k<4;)l=j*k,j=j*j-k*k-2+x/250,k=2*l-2+y/250,i++;c.putImageData(g,0,0);</script>``
