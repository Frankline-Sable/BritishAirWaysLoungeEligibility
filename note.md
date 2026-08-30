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


Tasks:
Run the cross-validation and give me the five scores + mean + standard deviation for:

accuracy, precision, recall, F1 and ROC-AUC.

Then give me your interpretation before I give you mine.

In particular, answer:

Is our balanced Random Forest consistently mediocre, consistently good, or is our earlier 80.36% / 22% recall result mostly an accident of one train/test split?

This is an important milestone: you're moving from “my model got X%” to “how strong is the evidence that my model actually generalizes?”


-----------------------------------
accuracy:
  folds: [0.8051 0.8037 0.808  0.8068 0.8111]
  mean: 0.80694
  std: 0.002542911716910382
precision:
  folds: [0.28584906 0.29181495 0.30586081 0.29739777 0.31196172]
  mean: 0.2985768602177127
  std: 0.009394904122520783
recall:
  folds: [0.20267559 0.21939799 0.22326203 0.21390374 0.21791444]
  mean: 0.21543075849981222
  std: 0.007046455612719967
f1:
  folds: [0.237182   0.25047728 0.25811437 0.24883359 0.25659189]
  mean: 0.2502398274031494
  std: 0.007414823814967687
roc_auc:
  folds: [0.64916242 0.65634997 0.64443565 0.665814   0.65421529]
  mean: 0.6539954670025689
  std: 0.007211353347171362

The scores across the 5 groups are generally well balanced, and  has less deviations, i can see the folds, improve consitently.
Thought the roc_auc is slightly average  and remains releatively stable.


feature_importance = pd.DataFrame({
    "feature": X.columns,
    "importance": balanced_model.feature_importances_
})

feature_importance = feature_importance.sort_values(
    "importance",
    ascending=False
)

feature_importance.head(15)



import matplotlib.pyplot as plt

top_features = feature_importance.head(15)

plt.figure(figsize=(10, 6))

plt.barh(
    top_features["feature"],
    top_features["importance"]
)

plt.gca().invert_yaxis()

plt.xlabel("Feature Importance")
plt.title("Top Features Influencing Booking Prediction")

plt.show()

accuracy 0.814
precision 0.368
recall 0.34
f1 0.353
roc_auc 0.745

| Model                    |  Accuracy | Precision |    Recall |        F1 |   ROC-AUC |
| ------------------------ |----------:|----------:|----------:|----------:|----------:|
| Basic                    |     80.7% |     29.9% |     21.5% |     25.0% |     65.4% |
| + booking origin         | **81.4%** | **36.8%** | **34.0%** | **35.3%** | **74.5%** |
| + booking origin + route |    82.27% |     40.1% |    37.48% |    38.74% |    78.33% |


How well does our model predict booking completion?
What information appears most useful?
What limitation should BA know about?


our model predicts booking completion using random forest classifier,
which has a balanced wieight and places greater feature importance on
purchase_lead as well length_of_stay ,flight_hour  and other features respectively to do the prediction
it has an accuracy of 82.27%
ROC-AUC os 78.33% meaning model is more than 70% more likely to rank completed bookings over non completed ones.

According to our feature importance analysis  the purchase_lead is really useful,
as well as the route, and book origins, which we noticed adding them signifactantly boosted our models prediction.

Limitation  is recall being less than average 37.48% meaning model can fail to identify more than half of customers who completed the bookings
