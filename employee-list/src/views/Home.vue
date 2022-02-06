<template>
  <div class="home">
    <newEmployeeBtn />
    <ul>
      <li v-for="(em,index) in employees" :key="index">
        {{em.name}}
      </li>
    </ul>
  </div>
</template>

<script>
import newEmployeeBtn from '../components/Home/newEmployeeBtn.vue'
import db from "../firebase/firebaseInit"
export default {
  name: 'Home',
  components: {
    newEmployeeBtn
  },
  data(){
    return{
      employees:[]
    }
  },
  created(){
    db.collection('employee').get().then(
      querySnapshot =>{
        querySnapshot.forEach(doc => {
          const data = {
            'id':doc.id,
            'employee_id':doc.data().employee_id,
            'name':doc.data().name,
            'dept':doc.data().dept,
            'position':doc.data().position,
          }
          this.employees.push(data)
        });
      }
    )
  }
}
</script>
