<template>
  <form>
    <div class="submit">
      <!-- <img style="height: 40px;" :src="this.image" :alt="unilagimg"> -->
      <a :href="this.url" class="link">MEET THE DEVELOPER</a>
      <h3>MIA UNILAG CGPA CALCULATOR</h3> 
    </div>

        <!-- NO OF COURSES -->
    <label>No. Of Courses:</label>
    <input type="number" placeholder="Number of courses you are offering" >

    <!-- COURSES -->
    <div>
      <label>Courses</label>
      <input type="text" placeholder="Your courses seperated by commas"  v-model="courses">
    </div>

    <!-- UNITS -->
    <div>
      <label>Course Units</label>
      <input type="number" placeholder="Course unit for each course" v-model="tempunit" @keyup="addunit"> 
      <div v-for="unit in units" :key="unit" class="pill">
        <span @click="deleteunit(unit)">{{ unit }}</span>
      </div>
    </div>

    <!-- GRADES  -->
    <div>
      <label>Grades</label>
      <input type="text" placeholder="Grade for each course => A=5 B=4 C=3 D=2 E=1 F=0" v-model="tempgrade" @input="addgrade">
      <div v-for="grade in grades" :key="grade" class="pill">
        <span @click="deletegrade(grade)">{{ grade }}</span>
      </div>
    </div>

    <!-- NO OF COURSES -->
    <label>First semeesther GPA:</label>
    <input type="number" placeholder='5.0' step='.01' required v-model="firstgpa">

     <!-- CALCULATE BUTTON  -->
    <div class="submit">
      <button @click="calculatecgpa (grades, units)">Calculate CGPA</button>
    </div>

  </form>

</template>

<script>
export default {
  data() {
    return {
      // image: 'download.png',
      url: "http://miaportfolio.netlify.app",
      tempgrade: '',
      grades: [],
      tempcourse: '',
      courses: '',
      tempunit: '',
      units: [],
      sumofgradeunit: 0,
      sumofunit: 0,
      gpa: 0,
      firstgpa: 4.9,
      cgpa: 0
    }
  },
  methods: {
    addgrade() {
      if(this.tempgrade) {
        this.grades.push(this.tempgrade)
        this.tempgrade = ''  
      }
    },
    deletegrade(grade) {
      this.grades = this.grades.filter((item) => {
        return grade !== item
      })
    },
    addunit() {
      if(this.tempunit) {
        this.units.push(this.tempunit)
        this.tempunit = ''
      }
    },
    deleteunit(unit) {
      this.units = this.units.filter((item) => {
        return unit !== item
      })
    },
    calculatecgpa (grades, units) {
      for(var i=0; i< grades.length; i++) {
        this.sumofgradeunit += grades[i] * units[i]
      }
      this.sumofunit = units.reduce((a,b) => {
        return  a + b }, 0)
      this.gpa = this.sumofgradeunit / this.sumofunit
      this.cgpa = ( this.firstgpa + this.gpa) / 2       
      return alert(`COURSES = ${this.courses} \n COURSE UNITS = ${this.units} \n GRADES = ${this.grades} \n GPA = ${this.gpa.toFixed(1)} \n CGPA = ${this.cgpa.toFixed(1)}`)
    }
  }
}
</script>

<style>
  form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px o 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  input[type='checkbox'] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
    color: blueviolet;
  }
  .pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }
  button {
    background: blueviolet;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    border-radius: 20px;
  }
  .submit {
    text-align: center;
  }
  h3, h4{
    color: blueviolet;
  }
  .link {
    text-align: center;
    color: white;
    background-color: blueviolet;

  }

</style>