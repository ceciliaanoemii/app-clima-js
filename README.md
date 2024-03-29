Aplicación de Clima.
App del clima utilizando JavaScript. La aplicación mostrará datos en tiempo real del clima de una ciudad específica utilizando la API de OpenWeatherMap.
Link a la pagina web: https://app-clima-by-ce.netlify.app/

<img width="416" alt="image" src="https://github.com/ceciliaanoemii/app-clima-js/assets/88951876/a9ea92e6-44bb-4c0e-8711-0dc1acef9014">

Consta de dos funciones principales: `fetchDatosClima(ciudad)` y `mostrarDatosClima(data)`. Aquí está cómo funciona cada una:

1.  `fetchDatosClima(ciudad)`: Esta función se encarga de hacer una solicitud a la API de OpenWeatherMap para obtener los datos del clima de la ciudad especificada. Recibe el nombre de la ciudad como parámetro. Utiliza la función `fetch()` para enviar una solicitud GET a la URL de la API, incluyendo la ciudad y tu clave de API. Luego, convierte la respuesta en formato JSON utilizando el método `json()`. Finalmente, llama a la función `mostrarDatosClima(data)` pasando los datos obtenidos como argumento.

    function fetchDatosClima(ciudad){
        fetch(`${urlBase}?q=${ciudad}&appid=${api_key}`)
        .then(data => data.json())
        .then(data => mostrarDatosClima(data))
    }
    
2.  `mostrarDatosClima(data)`: Esta función se encarga de mostrar los datos del clima en la página. Recibe los datos del clima en formato JSON como parámetro. Primero, obtiene las diferentes propiedades relevantes de los datos, como el nombre de la ciudad, el nombre del país, la temperatura, la humedad, la descripción y el icono del clima. Luego, crea elementos HTML apropiados, como encabezados y párrafos, y les asigna el contenido correspondiente utilizando la propiedad `textContent`. También crea un elemento de imagen para mostrar el icono del clima. Finalmente, agrega todos los elementos creados al elemento `<div>` con el ID "datosClima" en tu página.

    function mostrarDatosClima(data){
        const divDatosClima = document.getElementById('datosClima')
        divDatosClima.innerHTML=''
    
        const ciudadNombre = data.name
        const paisNombre = data.sys.country
        const temperatura = data.main.temp
        const humedad = data.main.humidity
        const descripcion = data.weather[0].description
        const icono = data.weather[0].icon
    
        const ciudadTitulo = document.createElement('h2')
        ciudadTitulo.textContent = `${ciudadNombre}, ${paisNombre}`
    
        const temperaturaInfo = document.createElement('p')
        temperaturaInfo.textContent = `La temperatura es: ${Math.floor(temperatura-difKelvin)}ºC`
        
        const humedadInfo = document.createElement('p')
        humedadInfo.textContent = `La humedad es: ${humedad}%`
    
        const iconoInfo = document.createElement('img')
        iconoInfo.src= `https://openweathermap.org/img/wn/${icono}@2x.png`
    
        const descripcionInfo = document.createElement('p')
        descripcionInfo.textContent = `La descripción meteorológica es: ${descripcion}`
    
        divDatosClima.appendChild(ciudadTitulo)
        divDatosClima.appendChild(temperaturaInfo)
        divDatosClima.appendChild(humedadInfo)
        divDatosClima.appendChild(iconoInfo)
        divDatosClima.appendChild(descripcionInfo)
    }
    
