<script>
    // let answer = JSON.parse(https://flamingo.spb.ru/patient.json)
    import moment from "../node_modules/moment"
    export default {
        components: {
            moment
        },
        data() {
            return {
                jsonData: [],
                receivedPatients: [],
                selectedPatient: {
                    number: 0,
                    firstName: "",
                    lastName: "",
                    thirdName: "",
                    nameWithInitials: "",
                    date: Date,
                    phone: "",
                    email: ""
                },
            }
        },
         mounted() {
            fetch('https://flamingo.spb.ru/api/patient')
            .then(res => res.json())
            .then(data => this.jsonData = data)
            .catch(err => console.log(err.message))
        },
        methods: {
            setPatient() {
                this.selectedPatient.number = this.jsonData.number
                this.selectedPatient.firstName = this.jsonData.first_name
                this.selectedPatient.lastName = this.jsonData.last_name
                this.selectedPatient.thirdName = this.jsonData.third_name
                let firstInitial = this.jsonData.first_name.substring(0, 1) + "."
                let secondInitial = this.jsonData.third_name.substring(0,1) + "."
                this.selectedPatient.nameWithInitials = this.jsonData.last_name + " " + firstInitial + secondInitial
                let birthdate = new Date(this.jsonData.birth_date)
                this.selectedPatient.date = moment(birthdate).format('YYYY-DD-MM')
                this.selectedPatient.phone = this.jsonData.phone
                this.selectedPatient.email = this.jsonData.email

                let bindingArray = []
                bindingArray.push({
                    number: this.jsonData.number, 
                    firstName: this.jsonData.first_name, 
                    lastName: this.jsonData.last_name, 
                    thirdName: this.jsonData.third_name,
                    nameWithInitials: this.jsonData.last_name + " " + firstInitial + secondInitial,
                    date: this.jsonData.birth_date, 
                    phone: this.jsonData.phone, 
                    email: this.jsonData.email})
                if (this.jsonData.related_patients.length != 0) {
                    this.jsonData.related_patients.map(function(value, key) {
                        let birthdate = new Date(value.birth_date)
                        let firstInitial = value.first_name.substring(0,1) + "."
                        let secondInitial = value.third_name.substring(0,1) + "."
                        bindingArray.push({
                            number: value.number,
                            firstName: value.first_name, 
                            lastName: value.last_name, 
                            thirdName: value.third_name,
                            nameWithInitials: value.last_name + " " + firstInitial + secondInitial,
                            date: moment(birthdate).format('YYYY-DD-MM'), 
                            phone: value.phone, 
                            email: value.email
                        })
                    })
                }
                this.receivedPatients = bindingArray
            },
            updatePatient(number) {
                this.receivedPatients.map(element => {
                    if (number == element.number) {
                        this.selectedPatient.firstName = element.firstName
                        this.selectedPatient.lastName = element.lastName
                        this.selectedPatient.thirdName = element.thirdName
                        this.selectedPatient.date = element.date
                        this.selectedPatient.phone = element.phone
                        this.selectedPatient.email = element.email
                    }
                });
            }
        }
    }
</script>

<template>
    <button @click="setPatient">Загрузить</button>
    <ul>
        <li v-for="patient in receivedPatients" @click="updatePatient(patient.number)">{{ patient.nameWithInitials }}</li>
    </ul>
    <form action="">
        <input type="text" placeholder="Имя" v-model="selectedPatient.firstName">
        <input type="text" placeholder="Фамилия" v-model="selectedPatient.lastName">
        <input type="text" placeholder="Отчество" v-model="selectedPatient.thirdName">
        <input type="date" placeholder="Дата рождения" v-model="selectedPatient.date">
        <input type="tel" placeholder="Телефон" v-model="selectedPatient.phone">
        <input type="email" placeholder="Email" v-model="selectedPatient.email">
    </form>
</template>

<style>
html {
    margin: 0;
    padding: 0;
    overflow: hidden;
}
body {
    background: #3f3f3f;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
}
ul {
    list-style: none;
    padding: 0;
    display: flex;
    gap: 15px;
    margin: 0 0 30px;
}
li {
    background: #220036;
    padding: 5px 10px;
    border-radius: 15px;
    color: #fff;
    cursor: pointer;
    font-size: 18px;
}
li.active,
li:hover {
    background: #540085;
}
form {
    width: 500px;
    display: flex;
    flex-direction: column;
    gap: 15px;
    color: black;
}
input {
    padding: 10px;
    border-radius: 5px;
    font-size: 16px;
    border: none;
    outline: aqua;
    font-family: 'Helvetica', 'Arial', sans-serif;
}
button {
    margin-bottom: 25px;
    font-size: 16;
    border-radius: 5px;
    background-color: aqua;
}
</style>
