## International Airfare Price Predictions

#### DESCRIPTION
Conducting analysis on webscraped data from Norwegian Air Shuttle for various flight itineraries from the US to Europe. Building prediction model to assist with purchasing decisions. Model to be hosted on Amazon EC2 and accessible via Flask API application

#### AIRPORTS OF INTEREST 
US (ORIG): `LAX` Los Angeles | `OAK` Oakland | `JFK` New York City  
EU (DEST): `CPH` Copenhagen | `ARN` Stockholm | `LGW` London-Gatwick | `BCN` Barcelona

#### DATA COLLECTION
Webscrape using Python Requests and BeautifulSoup

#### ACKNOWLEDGEMENTS
All data collected is in adherence to Norwegian Air Shuttle Terms of Use and intended for personal, academic purposes only

</br>

***

</br>

## Predictive Linear Model Design
Outcome:      `prices_lowfare_usd`  
Predictive:  
`orig_port_coded`* `dest_port_coded`* `days_to_flight`* `depart_yr` `depart_mo` `depart_day` `duration_total_min` `stops`  
 
</br>

**NOTE:**  
`orig_port_coded`* 0 = JFK | 1 = LAX | 2 = OAK  
`dest_port_coded`* 0 = ARN | 1 = BCN | 2 = CDG | 3 = CPH | 4 = LGW  
`days_to_flight`* days from **June 2, 2019** to flight date

</br>

## EC2 Hosting
The predictive model is hosted on Amazon's EC2 and accessible via a Flask API (instructions below)


## Accessing Flask API  
NOTE: API server is currently stopped, please contact if you wish to reproduce  

Please follow the steps below to execute the API  
*Linux required*

+ To send a request to the API, use a `curl` command like the example below:  
`curl -H "Content-Type: application/json" -X POST -d '{"orig_port_coded":"0","dest_port_coded":"0","days_to_flight":"10","depart_yr":"2019","depart_mo":"6","depart_day":"13","duration_total_min":"750","stops":"1"}' "http://ec2-54-218-176-151.us-west-2.compute.amazonaws.com:5000/predict_airfare"`  

> The response should look like: `{airfare prediction: 432.46229}`

</br>

**To reproduce the API:**

+ Download the files in this repository

+ In your terminal, navigate to the **docker** folder directory and run `docker-compose up` to create your local server

+ If created successfully, you should see output lines with `flask_1 | ....` outputs but will *not* be returning a prompt

+ Open up a new terminal and navigate to the same **docker** directory

+ To check the status of the server run:
`curl https://localserver:5000/`  
The response should say: Server is up!

+ To then access model predictions, follow the steps above for *Accessing Flask API* but change the request command url (at the end) to say `http://localhost:5000/predict_airfare`
