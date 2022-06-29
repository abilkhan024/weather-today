<template>
    <div class="history-parent w-fit mx-auto p-[15px] rounded-[10px] bg-white ">
    <ul class="flex flex-col text-[18px]">
        <li v-for="city in cities" :key="city.id" class="my-[5px]">
        {{city.cityName}}
        <button class="history-btn ml-[40px] float-right rounded-[10px] px-[5px] bg-blue-400 text-white"><i class="fa-solid fa-magnifying-glass"></i></button>
        </li>
    </ul>
    </div>
</template>

<script>
export default {
    name: 'History',
    data() {
        return {
            cities: [
                {
                    cityName: 'Dubai'
                },
                {
                    cityName: 'Almaty'
                },
                {
                    cityName: 'Bern'
                },
            ]
        }
    },
    mounted(){
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
            console.log(userInput)  
        }
        Array.from(document.querySelectorAll('.history-btn')).forEach((el, index) => {            
            el.addEventListener('click', ev => {
                getWeather(this.cities[index].cityName)
            })
        })

    },
    methods: {

    }
}
</script>

<style scoped>
.history-parent{
    width: 400px;
}
@media screen and (max-width: 900px) {
    .history-parent{
        width: 80%;
    }
}
</style>