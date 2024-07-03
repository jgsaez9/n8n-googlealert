# n8n-googlealert
Información para n8n + Google Alerts

Código para limpiar las URLs antes de guardarlas en la base de datos:
```
let output = []; // Array para almacenar las URLs procesadas

// Iterar sobre todos los elementos de entrada
for (const item of $input.all()) {

    let urlsArray = item.json.urls; // Acceder al array 'urls'
    let cleanedUrlsArray = []; // Array para almacenar las URLs limpias

    // Iterar sobre cada URL en el array 'urls'
    for (let originalUrl of urlsArray) {
        if (typeof originalUrl === 'string') {
            // Eliminar el prefijo específico
            let cleanedUrl = originalUrl.replace("https://www.google.com/url?rct=j&sa=t&url=", "");
            // Decodificar la URL
            let decodedUrl = decodeURIComponent(cleanedUrl);
            // Eliminar todo lo que sigue a "&"
            let finalUrl = decodedUrl.replace(/&.*/, '');
            // Agregar la URL procesada al array 'cleanedUrlsArray'
            cleanedUrlsArray.push(finalUrl);
        }
    }

    // Agregar el array de URLs procesadas al array de salida
    output.push({ json: { "url": cleanedUrlsArray } });
}

return output;
```
