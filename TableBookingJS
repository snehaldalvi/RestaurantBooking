var express = require('express');
var Res = require('./models/res');
var bodyParser = require("body-parser");
var app = express();
var mongoose = require('mongoose');
var path = require('path');

app.use(bodyParser.json());

mongoose.connect('mongodb+srv://username:password@cluster0-rv9v1.gcp.mongodb.net/restaurent?retryWrites=true', { useNewUrlParser: true }, function(err){
    if(err){
        console.log('Not connected to the database');
    }else{
        console.log('Connection Established !!');
    }
});
// viewed at http://localhost:8080
app.use(express.static(__dirname + '/public'));
app.get('/', function(req, res) {
    res.sendFile(path.join(__dirname + '/index.html'));
});

app.get('/pages/reservations', function(req, res) {
	console.log("hello");
    res.sendFile(path.join(__dirname + '/pages/reservations.html'));
});

app.post('/book',function(req, res){
	console.log(Object.keys(req.body.queryResult.parameters));
	var x = Object.keys(req.body.queryResult.parameters);
	console.log(x[0]);
	//For Name
	if(x[0] == 'any'){
	rest = new Res();
	rest.name = req.body.queryResult.queryText;
		
	rest.save(function(err, result){
	if(err){
		console.log(err);
	}
	else{
		console.log('Name stored successfully');
		res.json({
			"fulfillmentText" : "Enter your expected arrival?"
		});

	}

	});
}

	if(x[0] == 'time'){
		console.log('hii from time');

		Res.findOneAndUpdate({'name':'Abhishek'},{$set:{ 'time': req.body.queryResult.queryText } },
   { upsert: true },function(err, result){
		if(err){
			console.log(err);
		}
		else{
			console.log(result);
			res.json({
			"fulfillmentText" : "Enter your preferred table no."
		});

			} 
	});
}
	//For table no.
	if(x[0] == 'number'){
		
		Res.findOneAndUpdate({'name':'Snehal'},{$set:{ 'tableno': req.body.queryResult.queryText} },
   { upsert: true },function(err, result){
		if(err){
			console.log(err);
		}
		else{
			console.log(result);
			res.json('tableno inserted successfully');
			} 
	});
}

});



app.listen(process.env.PORT || 8081, function() {
  console.log("Server up and listening");
});
