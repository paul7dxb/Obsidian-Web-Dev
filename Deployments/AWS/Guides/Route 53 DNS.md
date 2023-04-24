
# Register Domain

- Route 53
- Register Domain
- Add to cart and purchase
	- Enable privacy

# Creating Records

- Route 53
- Hosted Zones
- Select domain
- Create record
- Specify route and fill in record details
- Create

# Route 53 IP Ranges

- Required for [[9.1 - Route 53#Health Checks|Route 53 health checks]]
- All Route 53 IPs
	- [JSON list of IPs](https://ip-ranges.amazonaws.com/ip-ranges.json)

# Health Checks

- Route 53
- Health Checks
- Create Health Check
- Name
- Endpoint
	- IP address of EC2
	- Port
- Path / or /health if defined route in application
- Advanced
	- Standard or fast (10s)
	- Failure threshold
	- String lookup
	- Customize chekcer regions or use recommended
- Create alarm

## Calculated

- Health Check
- Status of other health checks
	- Specify health checks to monitor
	- Specify amount to be healthy with conditions

## CloudWatch alarm

- CloudWatch alarm
- Select region

# Health Check logs

- Health Checks
- Health Checkers


# Failover

- Create A records that will be primary or secondary
	- Routing Policy - Failover
	- In create record select "Failover record type"
	- Asosciate primary with a health check
	- Assign an ID


# Geolocation

- Route 53
- Create record
- Type (e.g A)
- Routing policy -> Geolocation
	- Set location
		- Countries
		- Continents

# Traffic Flow

- Route 52
- Traffic flow
	- Traffic Policies
- Create traffic policy
- Specify type of start point
- Connect to rule
	- Choose type
- Geoproximity can open a map and show routing based on routes

- Creates a Traffic Policy Record

# 3rd Party domain

- Instead of using Amazon registrar
- Use custom name servers on registrar DNS manager
	- Route 53 
	- Create a Public Hosted zone
	- Get list of name servers