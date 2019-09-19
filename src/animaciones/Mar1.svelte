<script>

    import { onMount } from 'svelte'

    import Paper from 'paper';
    
    let canvas    

    //Paper.install(window);
    let rowH = ( window.innerHeight * 0.9 ) / 10
    
    onMount(()=>{
      
      
        let frame;
        let count=0;

        //let rowH = 
        
        (function loop() {
            
            frame = requestAnimationFrame(loop);

            count++

            if(count%12==0) {

                let ola
                let olas = []

                let fondo = new Paper.Path.Rectangle(
                    new Paper.Point(0,0),
                    new Paper.Point(window.innerWidth,window.innerHeight),
                );

                fondo.fillColor = new Paper.Color(0.01,0.3,0.7+(count%130/1300));

                //Define array of paths (I've choose 12 because my multitouch table accept 12 touch max)
                for (var i = 0; i < 10; i++)
                {
                    ola = new Paper.Path();
                    
                    ola.strokeColor = new Paper.Color((i*count%90)/900,(i%8*13)/500,0.3+i/15);
                    ola.strokeWidth = rowH / 1.6;
                    for (var j = 0; j < 30; j++)
                    {
                        let point = new Paper.Point(
                            j*30,
                            (i*rowH) - Math.cos(j-count)*20 * Math.sin(
                                (j*2) + count%36)
                            )                
                        //let point = new Paper.Point(j*33,i*30+Math.sin(count%360+j*30))                
                        ola.add( point )
                        // ola.smooth()
                    }

                    olas.push(ola);
                }

            }
                
            
        }());

/*         return () => {
            cancelAnimationFrame(frame);
        };
 */       

            
        Paper.setup(canvas);

        
        
    })
    
</script>


<style>
	canvas {
		width: 100vw;
		height: 90vh;
		background-color: #eee;
	}
</style>


<canvas
id="canvas"
bind:this={canvas}
width={1000}
height={400}
resize>
</canvas>
