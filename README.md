# forecast.io.live
Wrapper for forecast.io API using Socket.IO

# How to install
    npm install forecast.io.live
    
# Server side

    var io = require('forecast.io.live')(Server, API_KEY[, Options]);

**Server** : http.Server instance. 

**API_KEY** : A valid api key. 

**Options** : An object, with the following properties :

    {
      timeInterval(ms),
      timeout(ms)
    }
    
<i>timeInterval</i> : The time between each API call.

<i>timeout</i> : timeout for each request.

# Client side

    socket.emit('subscribe', {
        lat: ,
        long: ,
        lang: ,
        units: ,
        .....
      });
    
**Note**: Just the `lat` and `long` properties are required, you can find all available options [here](https://developer.forecast.io/docs/v2#options).


You can subscribe to multiple streams, each one will be defined by its `lat` and `long` properties, so doing something like :

    socket.emit('subscribe', {
        lat: 37.8267,
        long: -122.423
      });
      
      socket.emit('subscribe', {
        lat: 37.8267,
        long: -122.423
      });
      
The second `emit` will be ignored, this is useful for saving useless API calls

to receive the data, just listen to the `forecast` event :

    socket.on('forecast', function(data){
        // here we will receive all data coming from each stream, we can then filter them by lat and long...
    });
    
to stop a given stream, we emit a `stop` event: 

    socket.emit('stop', {
        lat: 37.8267,
        long: -122.423
      });

  



  

