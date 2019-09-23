<script>

    import { onMount } from 'svelte'

    import Raphael from 'raphael';
    
    let canvas    

    let colW = window.innerWidth / 80
    
    const olas = []

    let currentWaiting = null
    let currentActive = null

    let ultimoClickX = 0
    let ultimoClickY = 0 

    let paper
    let variador = 0


    let lineas
    
    const inicializarLineas = () => {
        
        lineas = paper.set()
        
        let distancia

        let posicion = 0
        while (posicion < window.innerWidth) {
            distancia = Math.abs(ultimoClickX - posicion)
            variador = distancia > 10 ? 0 : distancia / 10  
            posicion += 4 - variador
            lineas.push(
                paper.path(`M ${posicion}, 0 L ${posicion}, ${window.innerHeight}`)
                .attr({stroke: "#ddd"})
            )
        }
    }

    const dibujarLineas = () => {
        
        let distancia

        let posicion = 0
        let i = 0

        if (!!ultimoClickX) {
            while (posicion < window.innerWidth) {
                
                distancia = Math.abs(ultimoClickX - posicion)
                variador = distancia > 30 ? 0 : distancia / 10
                
                posicion += 4 + variador

                // if( distancia < 30 ) {
                    lineas[i].animate({
                        path: `M ${posicion}, 0 L ${posicion}, ${window.innerHeight}`
                    }, 1000)

                // }

                i++
            }

            ultimoClickX = null
        }
    }

    onMount(()=>{
        
        paper= Raphael(0, 0, window.innerWidth, window.innerHeight);
        
        inicializarLineas()

        document.body.addEventListener("click",(e)=>{
            ultimoClickX = e.clientX
            ultimoClickY = e.clientY
            console.log(ultimoClickX, ultimoClickY)
            // dibujarLineas()
            // circle.attr({
            //     cx: mouseX,
            //     cy: mouseY
            // })
        })
        


        
        
        let frame;
        let count=0;

        

/*         return () => {
    cancelAnimationFrame(frame);
        };
 */       




        

        (function loop() {
            
            frame = requestAnimationFrame(loop);
            count++

            if( count % 30 == 0 ) {

            }
            // paper.clear()
            dibujarLineas()
            
        }());

        
    })
    
</script>


<style>

	.caja {
		width: 100vw;
		height: 90vh;
		background-color: #eee;
	}
    * {
        box-sizing: border-box;
    }
</style>


<!-- <canvas
id="canvas"
bind:this={canvas}
width={1000}
height={400}
resize>
</canvas> -->


<h1>
    Raphael
</h1>


<div class="caja"></div>