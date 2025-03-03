Ok, hi, Im Matheus, I´m brasilian, live here in Portugal about 2 and a half years
I started working very young, I was only 17.
I worked in several IT areas, PC maintenance, custumer support and among others;
But I see that I really liked programming.
so I started in 2014 in
dwebnet
there I was a developer that Participation in all phases of a system construction project, 
from requirements gathering to back-end / front-end. Construction of on-demand systems We had a mobile applications in JAVA, another apps in VB.NET and ASPNET (webforms)
I work with futebal scount systems, real estate auction(ôction), scheduler aapointment with a medical clinics, payment in street parking (parking meter(mítar))


After I received a job offer, I moved to south the Brasil, I lived in southeast, and I join to
Hiper
In Hiper I was a software development, and after I was a tech leader, we had a ERP to managing small retail, with a module administrative, inventory, financial, payments.
There was desktop system, and the target was turn all this online. to this we create a archteture based in microservice, we had a microservice to each bussinness module.
and the comunication veried beetween HTTP, AMQP (rabbit and a little bit with Kafka)

Movidesk
After in Movidesk its a CRM system, to managing and open tickets to company custumer supports.
I worked to create a chatbot application (it still runs there today), using the Artifitial inteligence (AI) talk with custumers, to the ticket does not reach the human attendant.
We used the google dialog API as an AI machine, and marjoritary rabbitMQ to talk chatting. we uned lambdafuctions, entity framework 
postgreessDB anythings in mongoDB too

and in 2020 I start work to a Portugal company. my actual company, but in a project to

Galp
(Galp in portugal is fuel and energy distributor, joao knows, Im sure)
(I worked there About 2 and a half years in Galp.)
There We building a Application to managing payments for Galp's systems (fuel pumps, electric recharges, gas, etc...), auto payments
we integrated our application with banking APIs from SIBS (in Portugal), and Santander (in Spain).
In a structure of microservices in .Net Core, 
I worked with infrastructure, creating and supporting the architecture, and code security (because, its involves money), working on CI/CD pipelines with AzureDevOps.
In support of cloud environments (AWS), 
we use the as Docker, LambdaFunctions, KMS, S3 among others...

Vodafone
And now I work to Vodafone Group, in a building Radio Antenna division.
We have a system to makes workflows to a building new or change equipments in a Antenna, and makes API communications with NOS, ericsson, vantage towers germany
and another internal areas in Vodafone group.
Now I use in with dotnet core, RabbiMQ, Sql servers, redis.


### CLEAN CODE
my code must be easy to read, understand.
Reusability, respect the solid principies, a Clear Flow of Execution

# S — Single Responsiblity Principle (Princípio da responsabilidade única)
A class must be specialized in a single subject and have only one responsibility within the software
The class must have a single task or action to work/perform.

# O — Open-Closed Principle (Princípio Aberto-Fechado)
Objects must be open for extension but closed for modification.
for exemple if I have a payment method with cash and card, I should create a class payment with a method calc,
and another two card and cash implementing this method with your particularities

# L — Liskov Substitution Principle (Princípio da substituição de Liskov)
A derived/son class must be substitutable for its base/father class.
if I need that my sings in the both class must be equal, but with your implementations.

# I — Interface Segregation Principle (Princípio da Segregação da Interface)
a class does not have to implement methods that are not necessary.
for exemple in the class payment that I mentioned the class card have a method to make the 
comunication with "card operator, VISA, MASTER, however" and its dont make sense in cash class.
the interface payment dont need to have a method comunication WithCardOperator this is a exclusive responsability to interface cardPayment

# D — Dependency Inversion Principle (Princípio da inversão da dependência)
that high-level modules should not depend on low-level modules.

can I give a exemple, I have a class to recovery a password, and this class need make a connection in db
This class open a connection in db its is wrong, because the responsability this class not is create connections,
I need a class exclusive to open/close db connections, to this inject this new class.


## MICROSERVICES
Easier to build and maintain applications.
Business Resources
Improved productivity and speed
Flexibility in the use of technologies and scalability
Autonomous and cross-functional teams

## APIS
REST Representational State Transfer
version control
the corrects use to verbs, get post put/patch and delete
patch to partial updates and put to overwhite everything

PERGUNTAS
How many times a week do I need to go to the office?

How is the access to the office? Is it possible to arrive by train?

Do we have the freedom to apply new technologies?
