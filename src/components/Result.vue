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
            document.querySelector('.parent-result').classList.remove('show')  
            const userInput = document.querySelector('.cityName').value
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
            getWeather()
        }
        else{
            alert('Write the city name in coresponding field')
        }
        
      })
      document.addEventListener('keydown', (e) => {
        if(event.key !== 'Enter'){return}
        if(document.querySelector('.cityName').value !== ''){
            getWeather()
        }
        else{
            alert('Write the city name in coresponding field')
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