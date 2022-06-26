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
        async function getWeather(){
            const userInput = document.querySelector('.cityName').value
            const lonLatRequest = `https://nominatim.openstreetmap.org/search/${userInput}?format=json`
            const wetherRes = await fetch(lonLatRequest)
            const wetherData = await wetherRes.json()
            const lon = wetherData[0].lon
            const lat = wetherData[0].lat
            const weatherRequest = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=0add19c65d238de8a19d9686c17f47f4`
            const responseFromWeather = await fetch(weatherRequest);
            const dataWeather = await responseFromWeather.json();
            document.querySelector('.parent-result').innerHTML = `${dataWeather.weather[0].main} | ${Number((dataWeather.main.temp-273.15).toFixed(1))}°C`;
            // document.getElementById("feelsLike").innerHTML ="Feels like - "+ Number((dataWeather.main.feels_like-273.15).toFixed(1)) + "°C";
            // document.getElementById("wind").innerHTML = "Wind: " + dataWeather.wind.speed + " M/S";
        }
        document.addEventListener('click', (e) => {
        const isItBtn = e.target.matches('.isBtn')
        if((!isItBtn)){
            return
        } 
        if(isItBtn){
            document.querySelector('.parent-result').classList.add('show')  
            console.log('btn clicked')
            getWeather()
        }
        
      })
      document.addEventListener('keydown', (e) => {
        if(event.key !== 'Enter'){return}
        if(document.querySelector('.cityName').value !== ''){
            getWeather()
            document.querySelector('.parent-result').classList.add('show')  
        }
        
      })
    },
    methods: {
    },
    data(){
        return {}
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