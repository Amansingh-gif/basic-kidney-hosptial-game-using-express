# basic-kidney-hosptial-game-using-express
const express= require('express')

const users=[{
    name:"john",
    kidneys:[{
        healthy: false,
    }]
   
    
},]
const app= express()
const port=3000

//for get request we use query parameters for input
app.get('/', function(req,res){
  const johnkidneys=users[0].kidneys
  const totalnumberofkidneys=johnkidneys.length;
  let numberofhealthykidneys=0;
  for(let i=0; i<totalnumberofkidneys; i++){
    if(johnkidneys[i].healthy){
        numberofhealthykidneys=numberofhealthykidneys+1;
    }
  }
  let numberofunhealthykidneys=0;
  numberofunhealthykidneys=totalnumberofkidneys-numberofhealthykidneys;
  res.json({
    totalnumberofkidneys,
    numberofhealthykidneys,
    numberofunhealthykidneys,
  })
})
app.use(express.json())
// for post request we are going to use body
app.post('/',function(req,res){
    const ishealthy= req.body.ishealthy;
    users[0].kidneys.push({
       healthy:ishealthy
    })
    res.json({
        msg:"done!"
    })
})
app.put('/',function(req,res){
    for(let i=0; i<users[0].kidneys.length; i++){
        users[0].kidneys[i].healthy=true;
    }
    res.json({});
})
app.delete('/',function(req,res){
    const newfreshkidneys=[];
    for(let i=0; i<users[0].kidneys.length; i++){
        if(users[0].kidneys[i].healthy==true){
            newfreshkidneys.push({
                healthy:false
            })
        }
    }
    users[0].kidneys=newfreshkidneys;
    res.json({
        msg:"done!"
    })
})
app.listen(3000);
