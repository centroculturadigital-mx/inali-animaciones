<script>

    import { onMount } from 'svelte'

    import Paper from 'paper';
    
    let canvas    
    let paper    

    //Paper.install(window);
    let colW = window.innerWidth / 80
    
    const olas = []

    const crearLineas = () => {
        
        let ola

        let fondo = new Paper.Path.Rectangle(
            new Paper.Point(0,0),
            new Paper.Point(window.innerWidth,window.innerHeight),
        );

        // fondo.fillColor = new Paper.Color(0.01,0.3,0.7+(count%130/1300));

        //Define array of paths (I've choose 12 because my multitouch table accept 12 touch max)
        for (var i = 0; i < 80; i++)
        {
            ola = new Paper.Path();
            
            ola.strokeColor = new Paper.Color((i%90)/900,(i%8*13)/500,0.3+i/15);
            ola.strokeWidth = 1;

            let separacion = canvas.clientHeight / 30;

            for (var j = 0; j < 30; j++)
            {
                let point = new Paper.Point(
                    (i*colW) - (
                        Math.cos(j)
                        * 5 *
                        Math.sin(
                            (j*2) % 36
                        )
                    ),
                    j * separacion
                )                
                //let point = new Paper.Point(j*33,i*30+Math.sin(count%360+j*30))                
                ola.add( point )
                // ola.smooth()
            }

            ola.smooth()

            olas.push(ola);

        }

    }



    onMount(()=>{
        
        
        let frame;
        let count=0;

        //let colW = 
        

/*         return () => {
    cancelAnimationFrame(frame);
        };
 */       


        const paper = Paper.setup(canvas);

        crearLineas()

        

        (function loop() {
            
            frame = requestAnimationFrame(loop);
            count++

            if( !! olas ) {

                let separacion = canvas.clientHeight / 30;

                if(count%1==0) {
                    for (var i = 0; i < 80; i++) {

                        let ola = olas[i];


                        for (var j = 0; j < 30; j++)
                        {

                            const segment = ola.segments[j];
                            
                            segment.point.x = (i*colW) - (
                                Math.cos(j)
                                * (count/10)%3000 **
                                Math.sin(
                                    (j*2) % 36
                                )
                            )

                            // segment.point.y = j * separacion

                        }
                        
                    }
                }

            }
                
            
        }());

        
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
