1. Register
feature for register. Schema user is:
>> endpoint POST : user/signup
>> req.body
{
  username: <user_username>(yourusername)  
  email: <user_email>,(wirya@gmail.com)
  password: <user_password>(yourpassword)
}
>>email,password : required
>>username minlength :6
>>password minlength :6
>>email must @

2. Login
feature login. Schema user is :
>> endpoint POST : user/signin
>> req.body
{
  email: <user_email>,
  password: <user_password>
}
>> if success you will get token to access other feature

3. User
when user registration, automatic user create Townhall and user will get medal, resource : 100 golds , 100 foods and 0 soldier. User just have one townhall

{
  username: <user_username>
  townhall: <user_townhall>  
  email: <user_email>,
  password: <user_password>,
  resources: {
    gold: 100,
    food: 100,
    soldier: 0
  }
  medal: 0
}

# To Know One data user
>>Endpoint GET: user/:userID
>> req.headers : token
example(token : yourtoken )
# Output:
# {
#   yourdata
# }

# To change or update data userf
>>Endpoint PUT : user/userID
>>req.headers : token 
example(token : yourtoken )
>>req.body :
{
    username: <user_username>
    townhall: <user_townhall>  
}

4. Market

cost for create Market is 30 golds dan 10 foods.
Then market can generate coins / product coins
Market will produce 1 gold/minute.
Market has a capacity of 20 golds.
1 User can create much market if have resource sufficient
you can name your market

Endpoint:

A >> to create a market
>> POST : user/market/:userID
>> req.headers : token 
example(token : yourtoken)
>>req.body :
{
    namemarket: <user_namemarket>
}

B >> to know user have list market
>> GET : user/market/list/:userID
>> req.headers : token
example(token : token when login(yourtoken) )

C >> to know one market and know how much coins was generate
>> GET : user/market/:marketID
>> req.headers : token
example(token : token when login(yourtoken) )

D >> to update and change name market  
>> PUT : user/market/:marketID
>> req.headers : token
>> req.body : 
{
  namemarket : <user_namemarket>
}

E >> to delete the market
>> req.headers : token
>> DELETE :  user/market/:marketID

F >> to collect coins in market and send to your resource
>> GET : user/market/:marketID/collect
>> req.headers : token

4. Farm

cost to create Farm is 10 golds and 30 foods. 
Farm will produce 1 food/minute. 
Farm has a capacity of 20 foods.
1 User can create much market if have resource sufficient
you can name your farm

Endpoint:

A >> to create a farm
>> POST : user/farm/:userID
>> req.headers : token 
example(token : yourtoken)
>>req.body :
{
    namefarm: <user_namefarm>
}

B >> to know user have list farm
>> GET : user/farm/list/:userID
>> req.headers : token
example(token : yourtoken )

C >> to know one farm and know how much coins was generate
>> GET : user/farm/:farmID
>> req.headers : token
example(token : yourtoken )

D >> to update and change name farm  
>> PUT : user/farm/:farmID
>> req.headers : token
>> req.body : 
{
  namefarm : <user_namefarm>
}

E >> to delete the farm
>> req.headers : token
>> DELETE :  user/farm/:farmID

F >> to collect foods in farm and send to your resource
>> GET : user/farm/:farmID/collect
>> req.headers : token

5. Barrack

cost to build Barrack is 30 golds dan 30 foods.
Barrack produce 1 soldier/minute. 
Barrack has capacity 10 soldiers.

1 User can create much market if have resource sufficient
you can name your barrack

Endpoint:

A >> to create a barrack
>> POST : user/barrack/:userID
>> req.headers : token 
example(token : yourtoken)
>>req.body :
{
    namebarrack: <user_namebarrack>
}

B >> to know user have list barrack
>> GET : user/barrack/list/:userID
>> req.headers : token
example(token : yourtoken )

C >> to know one barrack and know how much coins was generate
>> GET : user/barrack/:barrackID
>> req.headers : token
example(token : yourtoken )

D >> to update and change name barrack  
>> PUT : user/barrack/:barrackID
>> req.headers : token
>> req.body : 
{
  namebarrack : <user_namebarrack>
}

E >> to delete the barrack
>> req.headers : token
>> DELETE :  user/barrack/:barrackID

F >> to collect foods in barrack and send to your resource
>> GET : user/barrack/:barrackID/collect
>> req.headers : token

5. attack other user
User can attack other user for get the resource on Townhall their. success will be random 
between success and failure on the basis of success is determined based on the number of soldiers sent.

if attack success/attacker win :

attacker: get 5 medal
attacker: get half from golds dan foods on Townhall enemy/defender
defender: soldier will be 0

if attack failed/attacker lose :

attacker: half medal will be lost (round down, if current 5 will be 2)
defender: get 2 medal
defender: soldier will lost 20

>> EndPoint : 

>> POST : user/:userID/attack/:enemyID

>> Request Body:
  {
    soldierattack : <sendsoldier>
  }

Notes:

Soldiers on send, both successful and failed attacks will disappear.

>> other feature : 

Townhall just can accommodate 1000 golds, 1000 foods dan 500 soldiers.
User just  can create maximal 30 barracks.
Users with the number of soldiers on Townhall below 50 cannot be attacked.