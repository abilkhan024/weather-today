<template>
    <div class="parent-result w-fit bg-[#FFFFFF] p-[30px] rounded-[10px] text-[24px]  text-blue-600">
    Loading
    </div>

</template>

<script>
export default {
    name: 'Result',
    props: {
    },
    created(){
        var that = this
        async function getHistory(){
            const apiPath = 'http://localhost:8080/cities'
            const res = await fetch(apiPath)
            const data = await res.json()
            that.cities = data
        }
        getHistory()
        async function toHistory(userInput){
            const apiPath = 'http://localhost:8080/cities'
            const userInputRequest = {
                cityName: userInput
            }
            const res = await fetch(apiPath, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(userInputRequest)
            })
            const data = await res.json()
            that.cities.push(data)
        }
        async function getHistory(){
            const apiPath = 'http://localhost:8080/cities'
            const res = await fetch(apiPath)
            const data = await res.json()
            that.cities = data
        }
        async function getWeather(userInput){
            document.querySelector('.parent-result').classList.remove('show')  
            const lonLatRequest = `https://nominatim.openstreetmap.org/search/${userInput}?format=json`
            const wetherRes = await fetch(lonLatRequest)
            const wetherData = await wetherRes.json()
            if(wetherData[0] === undefined){
                alert('Apparently you misspelled city name')
                return
            }
            const weatherRequest = `https://api.openweathermap.org/data/2.5/weather?lat=${wetherData[0].lat}&lon=${wetherData[0].lon}&appid=0add19c65d238de8a19d9686c17f47f4`
            const responseFromWeather = await fetch(weatherRequest);
            const dataWeather = await responseFromWeather.json();
            document.querySelector('.parent-result').textContent = `${dataWeather.weather[0].main} | ${Number((dataWeather.main.temp-273.15).toFixed(1))}°C`;
            document.querySelector('.parent-result').classList.add('show')  
        }
        document.addEventListener('click', (e) => {
        const isItBtn = e.target.matches('.isBtn')
        if((!isItBtn)){
            return
        } 
        if(isItBtn && document.querySelector('.cityName').value !== ''){
            const userInput = document.querySelector('.cityName').value
            getWeather(userInput)
            toHistory(userInput)
            setTimeout(() => {
                that.$emit('city-added')
            }, 230);
        }
        else{
            alert('Write the city name in coresponding field')
        }
        
      })
      document.addEventListener('keydown', (e) => {
        if(event.key !== 'Enter'){return}
        if(document.querySelector('.cityName').value !== ''){
            const userInput = document.querySelector('.cityName').value
            getWeather(userInput)
            toHistory(userInput)
            setTimeout(() => {
                that.$emit('city-added')
            }, 230);
        }
        else{
            alert('Write the city name in coresponding field')
        }
        
      })
    },
    methods: {
    },
    data(){
        return {
            cities: []
        }
    }
        
}
</script>

<style scoped>
.parent-result{
    opacity: 0;
    transform: translateY(-10px);
    transition: opacity 150ms ease-in-out, transform 150ms ease-in-out;
}
.parent-result.show{
    opacity: 1;
    transform: translateY(0px);
}

</style>