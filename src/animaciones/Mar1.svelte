<script>

    import { onMount } from 'svelte'

    import Paper from 'paper';
    
    let canvas    

    //Paper.install(window);
    onMount(()=>{
      
      
        
        Paper.setup(canvas);

        let myPath
        let myPaths = []
        //Define array of paths (I've choose 12 because my multitouch table accept 12 touch max)
        for (var i = 0; i < 12; i++)
        {
            myPath = new Paper.Path();
            myPath.strokeColor = '#e0e0e0';
            myPath.strokeWidth = 30;
            for (var j = 0; j < 12; j++)
            {
                let point = new Paper.Point(j*30,i*40+j*20)                
                myPath.add( point )
            }

            myPaths.push(myPath);
        }
        
    })
    
</script>


<style>
	canvas {
		width: 100%;
		height: 100%;
		background-color: #eee;
	}
</style>


<h1>
    Mar 1
</h1>

<canvas
id="canvas"
bind:this={canvas}
width={1000}
height={400}
resize>
</canvas>
