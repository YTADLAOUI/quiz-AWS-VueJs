<template>
    <!-- ================== stepper  ================== -->
        <div class="containers">

            <ol class="stepper">
              <li class=" stepper__item">
                  <h7 :class="{'circle':true, 'circle-acitve':isactive, 'stepper__title':true, 'step-1':true}" >Step 1</h7>
                  <!-- <p class="c-stepper__desc">Some desc text</p> -->
              </li>
              
            <li class="stepper__item">
              <h7 :class="{'circle':true, 'stepper__title':true,'circle-acitve':active, 'step-2':true}">Step 2</h7>
              <!-- <p class="c-stepper__desc">Some desc text</p> -->
          </li>
          </ol>
        </div>
</template>

<script>
export default {
props :{
  isactive : Boolean,
  active: Boolean
}
}
</script>

<style>
.containers{
    margin-left: 110px;
    margin-right: 110px;
    
}
.stepper {
    display: flex;
    flex-wrap: wrap;
    margin-top: 23px;}
    
    .circle{
        background: #FFF;
        height: 30px;
        width: 70px;
        display: flex;
        justify-content: center;
        border-radius: 50px;
        border: 3px solid whitesmoke;
    }
    .stepper__item {
        display: flex;
        align-items: center;
        gap: 0.5rem;
    }
    .circle-acitve{
        border-color: green;
    }

.stepper__item:not(:last-child) {
    flex: 1;
}
.stepper__item:not(:last-child):after {
    content: "";
    flex: 1;
    height: 2px;
    background-color: #e0e0e0;
    margin-inline-end: 0.5rem;
}
</style>