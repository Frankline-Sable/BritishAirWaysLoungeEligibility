Category:
ARRIVAL_REGION+HAUL


Table
category, Total Seats, Tier 1 %, Tier 2%, Tier 3%
[Europe + SHORT], 1075500, 0.0, 5.571920037192004, 94.428079962808
[North America + LONG], 776567, 1.324547656544767 , 16.29080298287205, 82.38464936058318
[Asia + LONG], 197355, 1.305262091155532, 16.248891591294875, 82.4458463175496
[Middle East + LONG], 200647, 1.3007919380803101, 16.06552801686544, 82.63368004505425


Representative samples (5 flights from each category)
Category, Total Passengers, Tier 1 % , Est. Tier 1, Tier 2 %, Est. Tier 2, Tier 3 %, Est. Tier 3

[Europe + SHORT], 900, 0.0, 0, 8.666666666666668, 78, 91.33333333333333, 822
[North America + LONG], 1252, 2.5559105431309903, 32, 19.568690095846645, 245, 77.87539936102237, 975
[Asia + LONG], 1607, 1.3690105787181084, 22, 15.183571873055381, 244, 83.44741754822651, 1341
[Middle East + LONG], 1238, 3.231017770597738, 40, 19.547657512116317, 242, 77.22132471728594, 956





ARRIVAL_REGION : <StringArray>
['North America', 'Europe', 'Asia', 'Middle East']

HAUL : <StringArray>
['LONG', 'SHORT']


Numerical columns - num_passengers, wants_extra_baggage,wants_preferred_seat, wants_in_flight_meals, booking_complete, flight_duration, purchase_lead, length_of_stay, flight_hour
Categorical columns -sales_channel, trip_type, flight_day, route, booking_origin, route

Notice columns with a few possible values:
Yes like sales_channels has only 2 types of values, and there is greater friction to wards the Internet than Mobile
Also trip_type has 3 types of values, and RoundTrip completely dominates, with the very less popular being CircleTrip
Also columns  wants_extra_baggage, wants_preferred_seat and wants_in_flight_meals, have few values(binary) with the positive that is true, mostly  dominating in all


Columns with lots of different values:
Like booking_origin, whereby top 3 dominant is Australia, Malaysia and South Korea, the rest and closely tied together hence  leading to many different outcomes hence difficult to classify
Also on the route dominant being AKLKUL its difficult to rely on this for classification, since the values are not that spaced apart, this applies to light day as well.


Suprises:
According to the dataset I have noticed most people most people like to book individually,
with the number of bookings decreasing almost exponentially as customer count perbooking increases.

As we have also noticed people prefer booking on the internet than on mobile, as well as RoundTrip significantly dominating the other types of trips

The weekends are the least booked, and mondays are the most bookings

Australia customers dominates in booking, followed by malaysia

Most people want wants_extra_baggage and wants_preferred_seat, 

Most people prefer booking longer flight durations.


Also noticed max number of passengers per booking is 9, rarely goes past 9
with the minimum being mostly 2.


Sales channel hypothesis, i had noticed there are significant booking attempts on Internet than mobile
and finding the mean observed that there is 15.5% booking completion on internet than on mobile which is 10.1%

Definately trip_type is related to completion, like roundtrip has 15% completing, compared to the rest which have less than 5% completion


Initially we observed monday to have the highest booking attempts, but observed that highest completion day was on wed followed by thursday




Customers with positive pref are more than 15% likely to complete a booking 
Customers who attempt longer flight duration are less likely to complete the booking
but longest flight_hour are more likely to complete booking, but not a big variation



Customers who have lower purchase_lead and length_of_stay appear more likely to complete because perhaps they dont want to stay long.
Customers who have applied to atleast one of the extra features appear more likely to complete because perhaps this insights to complete a booking.



Customers who positive preferences appear more likely to complete because perhaps _____.
Customers who _____ appear more likely to complete because perhaps _____.
Customers who _____ appear more likely to complete because perhaps _____.



binary - two states
norminal - no meanful order
ordinal - with a meaning full order

One hot encoding


sales_channel - binary
trip_type -  norminal
flight_day - ordinal, mon to sunday the day increases, where mon=1 and sun=7
route - norminal
booking_origin- norminal
wants_extra_baggage - binary

cycle encoding

models takes X and Y
X- featurs
Y - target

High cardinality

model overfitting- weak evidence

high cardility: one hot encoding, frequency encoding,
grouping rare categories, target encoding, feature engineering from routes,
ropping a feature and others

biz cares about identifying customers likely to complete a booking not just the accuracy,
Imbalanced datasets force us to think beyond accuracy,

balance vs imbalanced-> accuracy validility


100 customers.
85 - N
15 - Y

80 - N
10 - Y

80+10/100*100=90%

            actual true,  actual false
pred true    TP              FP
pred false   FN               TN

TP=10
FP=5
FN =5
TN =80


F1 combines  both precision ad recall,

if recall is poor f1 will aslo be poor




               Original    Balanced
Accuracy          84.71%       80.36%
Class 1 Precision   43%        29%
Class 1 Recall       6%        22%
Class 1 F1          11%        25%
False Negatives    1402        1170
True Positives       94        326



Balancing helped us find more completed bookings, but still the False Negatives are a bit high.
The accuracy as well as precision reduced while the recall increased, meaning this model be was bit better at identifying most consumers who ultimately completed a booking.


(21%+22%+20%+23%+21%=107%)/5=21.4
5%, 45%, 12%, 38%, 9% =21.8%


I have observed model B has a has higher mean score than model A, that is Score for Model B is 21.8% and for model A is 21.4%
But the variations in the recall in model B is quite poor, while in model A is much balanced, for this reason I wouldn't trust model B with new customers and would prefer model A

