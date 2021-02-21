# tiny-mandelbrot

A variable resolution Mandelbrot visualizer for the JS canvas in just 262 bytes

Change the Query String of the URL, to change the resolution (e.g. https://missing-user.github.io/tiny-mandelbrot#2000 for 2000x2000px)

Check it out! https://missing-user.github.io/tiny-mandelbrot#1000

The full code:
``<canvas id=a><script>for(c=a.getContext`2d`,a.height=a.width=h=location.hash.substr(1)||1e3,g=c.createImageData(h,h),m=g.data,o=3,y=h;y--;)for(x=h;x--;m[o+=4]=i)for(i=j=k=0;i<255&j*j+k*k<4;)l=j*k,j=j*j-k*k-2+4*x/h,k=2*l-2+4*y/h,i++;c.putImageData(g,0,0)</script>``
