<template>
  <div class="FormApp">
    <form @submit.prevent="submitted">
  <div class="container-fluid">
    <div class="submittedModal" :class="[cond == false? 'formblock' :'']">
      <div class="col-md-12">
        <h2>Your form has been submitted successfuly .. the form informations is:</h2>
        <p>Mood: <span> {{mood}} </span> <br>
        stress: <span> {{stress}} </span><br>
        shift: <span> {{shift}} </span><br>
        location: <span> {{location}} </span><br>
        comment: <span> {{comment}} </span></p>

      </div>      
    </div>

    <div class="row"> 
      <div class="col-md-12 header"><h1> Mood tracker</h1></div>
    </div>
      <div :class="[cond == true? 'formblock' :'']">
        
      <div class="row">
        <div class="col-md-12">
            <!-- Mood Tracker -->
            <h2> Mood Level </h2>
            <circle-slider :side="200" :circle-width-rel="15" :min="0" :max="101" :step-size="1" circle-color="#554AC9"
            progress-color="#FDC84A"
            knob-color="#FDC84A" v-model.lazy="moodSlider"></circle-slider>
            <img class="img" :src="'../../static/emojies/mood'+mood+'.png'" width="100%">      
      </div>
      
        <div class="col-md-12">
    
            <!-- stress Tracker -->
            <h2> Stress Level</h2>
            <circle-slider :side="200" :circle-width-rel="15" :min="0" :max="101" :step-size="1" circle-color="#554AC9"
            progress-color="#FDC84A"
            knob-color="#FDC84A" v-model="stressSlider"> </circle-slider>
            <img class="img" :src="'../../static/emojies/stress'+stress+'.png'" width="100%">
          </div>
      </div>
      
      <div class="row"> 
        <div class="col-md-12 rule"> <h2 :class="[error == true? 'error' : '']"> What is your Rule </h2>
          <label class="radioStyle" v-for="item in ruleText" v-bind:key="item">
            <input type="radio" name="options" :value="item" v-model="rule"> 
            <span class="radioText"> {{item}} </span>
          </label>
        </div>
      </div>

      <div class="row">
        <div class="col-md-3"></div>
        <div class="col-md-6">
        
        <div class="shift">
          <h2 :class="[error == true? 'error' : '']">When is your Shift ?</h2>
          <div class="left">
        <label class="radioStyle">
          <input type="radio" name="radio" value="Night" v-model="shift">
          <span class="checkmarkl"><i class="far fa-moon fa-2x"></i></span>
        </label>
        </div>
        <div class="clear"></div>
        <div class="right">
        <label class="radioStyle">
            <input type="radio" name="radio" value="Day" v-model="shift">
            <span class="checkmarkr"><i class="far fa-sun fa-2x"></i></span>
          </label> 
          </div>
          </div> 
        </div>
        
        <div class="col-md-3"></div>
        </div>

        <div class="row">
          <div class="col-md-3"></div>
        <div class="col-md-6 "> 
          
        <div class="location">
          <h2 :class="[error == true? 'error' : '']">Where is you location ?</h2>
          <div class="up">
        <label class="radioStyle">
          <input type="radio" name="radio2" value="North" v-model="location">
          <span class="checkmarks"><i class="fas fa-long-arrow-alt-up fa-2x"></i></span>
        </label>
        </div>
        <div class="down">
        <label class="radioStyle">
              <input type="radio" name="radio2" value="South" v-model="location">
              <span class="checkmarkn"><i class="fas fa-long-arrow-alt-down fa-2x"></i></span>
        </label>
        </div>
            </div>
        </div>
        <div class="col-md-3"></div>
      </div>

      <div class="row"  style="margin-top:220px;">
        <div class="col-md-2"></div>
        <div class="col-md-8">
          <label for="validationTextarea"> <h2 :class="[error == true || comment == ''? 'error' : '']"> Do you have Any comments? </h2> </label>
          <textarea class="form-control textarea" name="textarea" id="validationTextarea" placeholder="Tell us something new about yourself" rows="5" v-model="comment"></textarea>
          <div class="col-md-12" style="text-align:left; font-size:13px;">     
            <label for="defaultCheck1" :class="[error == true? 'error' : '']">    
            <input type="checkbox" value="agree" v-model="disclaimer">          
            Disclaimer - The IGNITE Mood Tracker application is intended for informational, educational and research purposes only.
           </label>
           </div>
          <button type="submit" class="btn btn-lg btn-success btn-submit" value="submit">Submit</button>
          <button type="reset" class="btn btn-lg btn-danger btn-submit" value="reset">Reset</button>
        </div>
        <div class="col-md-2"></div>
      </div>
      
      </div>
    </div>
    </form>
  </div>
</template>

<style scoped>
@import "../assets/style.css";
</style>

<script>
export default {
  data () {
    return {
      error: false,
      cond: false,
      disclaimer: null,
      mood: null,
      moodSlider: null,
      stressSlider: null,
      stress: null,
      rule: null,
      shift: null,
      location: null,
      comment: null,
      ruleText: [ 'Physician (MD)',
        'Nurse Practitioner (APN)',
        'Nurse (RN)',
        'Certifed Nursing assistant (CNA)',
        'Respiratory Therapist (RT)',
        'Pharmacist',
        'Registered Dietition (RD)']
    }
  },
  watch: {
    moodSlider: function (moodSlider) {
      if (moodSlider > -1 && moodSlider < 10) {
        this.mood = 0
      } else if (moodSlider > 9 && moodSlider < 20) {
        this.mood = 1
      } else if (moodSlider > 19 && moodSlider < 30) {
        this.mood = 2
      } else if (moodSlider > 29 && moodSlider < 40) {
        this.mood = 3
      } else if (moodSlider > 39 && moodSlider < 50) {
        this.mood = 4
      } else if (moodSlider > 49 && moodSlider < 60) {
        this.mood = 5
      } else if (moodSlider > 59 && moodSlider < 70) {
        this.mood = 6
      } else if (moodSlider > 69 && moodSlider < 80) {
        this.mood = 7
      } else if (moodSlider > 79 && moodSlider < 90) {
        this.mood = 8
      } else if (moodSlider > 89 && moodSlider < 100) {
        this.mood = 9
      } else if (moodSlider === 100) {
        this.mood = 10
      }
    },
    stressSlider: function (stressSlider) {
      if (stressSlider > -1 && stressSlider < 10) {
        this.stress = 0
      } else if (stressSlider > 9 && stressSlider < 20) {
        this.stress = 1
      } else if (stressSlider > 19 && stressSlider < 30) {
        this.stress = 2
      } else if (stressSlider > 29 && stressSlider < 40) {
        this.stress = 3
      } else if (stressSlider > 39 && stressSlider < 50) {
        this.stress = 4
      } else if (stressSlider > 49 && stressSlider < 60) {
        this.stress = 5
      } else if (stressSlider > 59 && stressSlider < 70) {
        this.stress = 6
      } else if (stressSlider > 69 && stressSlider < 80) {
        this.stress = 7
      } else if (stressSlider > 79 && stressSlider < 90) {
        this.stress = 8
      } else if (stressSlider > 89 && stressSlider < 100) {
        this.stress = 9
      } else if (stressSlider === 100) {
        this.stress = 10
      }
    }
  },
  methods: {
    submitted: function () {
      if (this.rule == null || this.shift == null || this.location == null || (this.comment == null || this.comment === '') || this.disclaimer == null) {
        this.error = true
        alert('You have to check your inputs please')
      } else {
        this.cond = true
        /* alert('Your Form has submitted .. Mood is: ' + this.mood + ' / Stress is: ' + this.stress +
        ' / Your rule is: ' + this.rule + ' / Your shift in: ' + this.shift +
        ' / Your location in: ' + this.location + ' / Your comment is: ' + this.comment) */
      }
    }
  }
}

</script>
<style scoped>
  
  .error::before{
    color: red;
    content: '* ';
  }
  
</style>
