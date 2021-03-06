---
layout: project
title: thesis
time: 2014-2015
heading: An exciting collaboration with Radu Darie in the Borton Neuromotion Laboratory at Brown University. We created a tool to predict movement from spinal cord stimulation in primates. The project was built in modular fashion to allow for continuous development, and the Borton laboratory has continued to build on the project. 
tags:
    - neuro-engineering
    - modeling
    - predictive modeling
    - system design
theme: '#1C85FF'
infotextcolor: white
type: coursework / group
custom_js:     
    -  "/assets/scripts/project.js"
---


<section class="intro block">
    <div class="intro-text block-text">
        <p style="text-align: center; color: blue"> Design a tool to simulate the (physical) effect of spinal cord stimulation in primates.
        </p>
    </div>
</section>

<section class="block">
    <header class="block-header">context</header>
    
    <div class="block-text">
        <p>Spinal cord injury - affects 250,000 americans/year, and can cause devastating, irreversible motor deficit. Currently, there are no viable treatments for re-generating movement due to lost motor control.</p>  
    </div>
    
    <div class="block-text layered">
        <p>
        Current treatment - Epidural Electrical Stimulation (EES) of the spinal cord has shown to improve motor control in humans and animals with spinal cord injury.<span class="info-tooltip">Zapping the spinal cord can actually induce controlled movement. Motor signals can be reduced to (convoluted) electrical pathways. Though our understanding of these pathways is rudimentary, neuro-engineers have been able to manipulate these pathways using neural implants and electrodes to produce constrained movement. </span>
        </p>
    </div>
    
    <div class="block-text layered">        
        <p>
        The end goal of EES research is to develop a closed-loop system where neural implants can translate intention to move -> electrical stimulation -> actual movement. Currently, neural implants do receive feedback from muscle and neural recordings - but these signals are only decoded with low fidelity. <span class="info-tooltip">A fully closed-loop system would necessitate having a thorough understanding of neural pathways to stimulate, as well as rigorous method of decoding thoughts. Brain control is a distant, but possible reality...</span>
        </p>
    </div>  
    
    <div class="block-image-container">
        <img src="/assets/img-thesis/thesis-experiment.png" class="block-image block-image-medium">    
    </div>          
      
    <div class="block-text">
        <p>Although devices to stimulate, record, and interpret electrical signals from movement are reliable, the exact input parameters and locations for stimulation devices are not usually known for experiments involving primates. <span class="highlight-grey">Researchers rely on visual/empirical observation for stimulation, which is unreliable and cruel to test animals</span>
        </p>
   </div>
   
   <div class="block-text layered">
        <p>
        Experimental simulations are a logical, and crucial next step in developing neuroprosthetic systems. 
        <span class="info-tooltip">
        Simulations will present some semblance of machine learning to spinal cord stimulation experiments. Instead of relying on intuition for determining electrode placement and stimulation strength, researchers will guide their experiments with constrained, incremental changes from a centralized model. 
        </span>
        </p> 
    </div>      
</section>


<section class="block">
    <header class="block-header">use case</header>
    <div>
        <p>
        Creating a tool for EES simulation entails re-creating the spinal cord (physically and biologically) from scratch. As you might imagine, our end product does not come close in complexity to an actual primate spinal cord. It does however, provide a <span class="highlight-grey">functioning framework of an EES experiment</span>. Users can place an electrode in a physically-accurate spinal cord, run a simulation, and determine which motor fibers were recruited as a result of the virtual experiment.
        <br><br>
        We ensured that our computational model was <a href="https://github.com/penguinscontrol/Spinal-Cord-Modeling"  class="underline">well-documented</a> to allow for other researchers to use the model and build on it. As more EES experiments are conducted, our model will have more data to draw from, and become more accurate. Though the project is no longer in my hands, the Borton Lab has continued development
        </p>
    </div>      
    <div class="block-image-container">
        <img src="/assets/img-thesis/img-thesis.png" class="block-image block-image-small">
    </div>    
</section>

<section class="block">
    <header class="block-header">process</header>
    <div class="block-text">
        <p> 
        We used three pieces of software to create a hybrid physical-neural model of the spinal cord.
        <span class="info-tooltip">
        Current software can be used to create physics simulations, or neural simulations, but not both. We used MATLAB to mediate between a finite element model (physical model) constructed on COMSOL, and a neural model created on NEURON software.
        </span>        
        </p> 
        <p>
        After developing and validating a functional hybrid model, we worked to make our model modular and scalable.
        </p>
    </div>      
    <div class="block-image-container">
        <img src="/assets/img-thesis/thesis-process.png" class="block-image block-image-medium">    
    </div>  
</section>


<section class="block">
    <header class="block-header">physical model</header>
    <div class="block-text layered">
    <div style="clear:both"></div>
        <p>Drawing - was the first step in constructing our physical FEM model. We used images and dimensions of histological spinal cord slices as a blueprint for rendering a biologically-accurate spinal cord. 
        <span class="info-tooltip">
        Conductivity values were assigned to different layers of the spinal cord to ensure that it could emulate a real stimulation experiment. Note that this model is simply a volume conductor - and does not actually have any neurons! Neurons were later superimposed onto the model.</span> </p>  
    </div>      
    <div class="block-image-container">
        <img src="/assets/img-thesis/thesis-finiteelement.png" class="block-image block-image-medium">    
    </div>      
    <div class="block-text">
        <p>      
        We tested our model by running simulations, and, simply, doing the math. Each 3D spinal cord component to be imported into COMSOL, a physics simulator, as a volume conductor. Our electrode, approximated as a surface current source, was placed in the epidural space to imitate EES experiments. (Later on, electrode placement was reduced to a simple parameter in MATLAB, allowing for quicker iteration in determining electrode placement). 
        </p>
    </div>
    <div class="block-text layered">  
        <p>
        Our model matched mathematical predictions. 
        <span class="info-tooltip">The graph below bears a 1/r relationship of voltage, which resembles Maxwell's equations.  Given that current and conductivity (equation 1) are constant, distance from the source is responsible for the relationship shown. At the top center of the graph (dark area), the distance to the point source is lowest, and voltage is at a maximum). Anatomically, we see the same patterns that were demonstrated in real experiments: the highest concentration of current in the epidural space, with a large voltage drop-off in the CSF, and some current carried over into the dura.</span>       
        </p>  
    </div>          
    <div class="block-image-container">
        <img src="/assets/img-thesis/thesis-voltage-distribution.png" class="block-image block-image-medium">    
    </div>      
</section>

<section class="block">
    <header class="block-header">neural model</header>
    <div class="block-text">
        <p>Our neural model was written in .hoc, a scripting language built for NEURON (biophysical neural network modeling software). NEURON enables users to instantiate neural elements like fibers and axons as objects, and run simulations 
        </p>     
    </div>     
    <div class="block-text layered">
         <p>Validation - in line with experimental procedures, the electrical stimulation is visualized as a square wave pulse. Additionally, plots of Ia axon and motor neuron display the typical signature of an action potential.
         <span class="info-tooltip">
           Threshold, depolarization, repolarization, and refractory period phases are clearly shown. The motor neuron, pictured in orange, is recruited after the Ia fiber, which is expected given that the motor neuron is stimulated indirectly. At low stimulation values (200 mA and less), neither the Ia axon, nor the motor display peaks, as expected.         
         </span>
        </p>
    </div>
    <div class="block-image-container">
        <img src="/assets/img-thesis/thesis-neural.png" class="block-image block-image-medium">    
    </div>  

</section>

<section class="block">
    <header class="block-header">integrated model</header>
    <div class="block-text">
        <p>Model structure - <br>Using MATLAB, we integrated our physical (finite element) and neural models. At the user level,  MATLAB code carries biophysical and electrical parameters of stimulation, relevant plots, and debugging tools. Running a simulation with our model demands that the user interacts with MATLAB (as MATLAB probes COMSOL and NEURON for values). 
        </p>  
    </div>
    <div class="block-text">   
        <p>
        Model mechanics -  
        <br>

        We wrote a MATLAB script to generate geometric points representing fibers in the spinal cord. This geometric axon was transposed onto the Finite Element model, where voltage values along nodes of the axon (corresponding to points along internode intervals) are written to a text file. COMSOL-generated voltage values, along with electrical and biophysical parameters, are fed to NEURON (through the command line, and text files), where a biophysical simulation is run using realistic electrical values. Results from the NEURON simulation are written to a text file, which serve as the basis for a MATLAB plot of the recruitment curve. 
     
        </p>
    </div>   

    <div class="block-image-container">
        <img src="/assets/img-thesis/thesis-transposed.png" class="block-image block-image-small">    
    </div>   
    <div class="block-text">
        <p>Validation - our computational model (like those in research literature) was built under the assumption that the number of motor axons recruited is proportional to a motor potential produced by an EES stimulus [Capogrosso]. This assumption entails that the recruitment curve – a plot of neuron firing as a result of stimulation – is a valid metric for evaluating model efficacy. 
        <br><br> 
        </p>
    </div>
    <div class="block-text layered">
        <p>    
        The recruitment curve below shows the same sigmoidal shape that is described in literature studies using the same diameter distribution. <span class="info-tooltip">The graph below reveals typical characteristics of a recruitment curve that Capogrosso and Vleggert-Lankamp describe [PAPER]. The slope of this sigmoid shape is a result of our diameter distribution — larger diameter fibers are the first to be recruited, and smaller fibers are gradually recruited afterwards. We also see a flat-line preceding a certain threshold voltage, a positive slope where fibers start to reach threshold and elicit action potentials, and a peak value where all fibers are recruited.
        </span>
        </p>  
    </div>        
    <div class="block-image-container">
        <img src="/assets/img-thesis/img-integrated.png" class="block-image block-image-medium">    
    </div>    
</section>

<section class="block">
    <header class="block-header">optimization</header>
    <div class="block-text">
        <p>In order to ensure that our model would be scalable, we integrated our NEURON script with the MPI parallel simulation environment, enabling parallel simulations (on multi-core processors).
        </p>  
    </div>     
    <div class="block-image-container">
        <img src="/assets/img-thesis/thesis-parallelization.png" class="block-image" style="max-width: 550px">     
    </div>
    <div class="block-text"> 
    </div>
</section>






