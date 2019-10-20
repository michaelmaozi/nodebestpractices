# Usar Async-Await o promises para capturar errores asíncronos

### Párrafo de explicación

Los callbacks no escalan bien ya que muchos programadores no están familiarizados con ellos. Te obligan a estar pendiente de errores por todos lados y a lidiar con un anidamiento de código excesivo, lo cual dificulta la comprensión del flujo de código. Librerías prometedoras como BlueBird, async y Q empaquetan un estilo de código estándar utilizando RETURN y THROW para controlar el flujo del programa. Específicamente, soportan el estilo favorito de gestión de errores try-catch, liberando a la ruta principal de código de tratar con errores en cada función.

### Code Example – using promises to catch errors

```javascript
doWork()
 .then(doWork)
 .then(doOtherWork)
 .then((result) => doWork)
 .catch((error) => {throw error;})
 .then(verify);
```

### Anti pattern code example – callback style error handling

```javascript
getData(someParameter, function(err, result) {
    if(err !== null) {
        // do something like calling the given callback function and pass the error
        getMoreData(a, function(err, result) {
            if(err !== null) {
                // do something like calling the given callback function and pass the error
                getMoreData(b, function(c) {
                    getMoreData(d, function(e) {
                        if(err !== null ) {
                            // you get the idea? 
                        }
                    })
                });
            }
        });
    }
});
```

### Blog Quote: "We have a problem with promises"

 From the blog pouchdb.com

 > ……And in fact, callbacks do something even more sinister: they deprive us of the stack, which is something we usually take for granted in programming languages. Writing code without a stack is a lot like driving a car without a brake pedal: you don’t realize how badly you need it until you reach for it and it’s not there. The whole point of promises is to give us back the language fundamentals we lost when we went async: return, throw, and the stack. But you have to know how to use promises correctly in order to take advantage of them.

### Blog Quote: "The promises method is much more compact"

 From the blog gosquared.com

 > ………The promises method is much more compact, clearer and quicker to write. If an error or exception occurs within any of the ops it is handled by the single .catch() handler. Having this single place to handle all errors means you don’t need to write error checking for each stage of the work.

### Blog Quote: "Promises are native ES6, can be used with generators"

 From the blog StrongLoop

 > ….Callbacks have a lousy error-handling story. Promises are better. Marry the built-in error handling in Express with promises and significantly lower the chances of an uncaught exception. Promises are native ES6, can be used with generators, and ES7 proposals like async/await through compilers like Babel

### Blog Quote: "All those regular flow control constructs you are used to are completely broken"

From the blog Benno’s

 > ……One of the best things about asynchronous, callback-based programming is that basically all those regular flow control constructs you are used to are completely broken. However, the one I find most broken is the handling of exceptions. Javascript provides a fairly familiar try…catch construct for dealing with exceptions. The problem with exceptions is that they provide a great way of short-cutting errors up a call stack, but end up being completely useless of the error happens on a different stack…