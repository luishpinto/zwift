# ZWIFT CUSTOMIZED TRAINING based on a COOPER TEST

The attached file labeled **zwo_file.ipynb** is a relatively easy program able to create **.zwo** files used in **ZWIFT Customized Trainig Session**.

The programs is based on two classes:
  1. the Cooper class with the runner features like: age, weight, VO2Max, HR and pace zones, etc.;
  2. the Header class with the header features like: author, title and description of the customized training.
  
The procedure to implement a new customized training is prety simple:

## 1<sup>st</sup> step -- Define the file-header

Define a variable **fh** with the file-header data, according to the following procedure:

```
fh = Header(author = 'AUTHOR',
            name = 'NAME OF THE TRAINING SESSION',
            description = 'DESCRIPTION OF THE TRAINING SESSION')
```

for example:

```
fh = Header(author = 'Luis H PINTO',
            name = 'ONE-MILE THRESHOLD',
            description = 'Half Marathon PHASE II: WEEK 8 | 3 x ( 1.70 T + 0.40 E)')
```

## 2<sup>nd</sup> step -- Input the runner features and the result of the Cooper Test

As the most part of the runners know, a **Cooper Test** is usually performed in a flat-track with a 5-minutes warming up and a 12-minutes **AS-FAST-AS-POSSIBLE**, registering at the end the **distance** covered.

Define a variable **df** with the runner-features, according to the following procedure:

```
df = Cooper(age = AGE,
            weight = WEIGHT,
            distance = DISTANCE COVERED DURING THE COOPER TEST)
```

for example:

```
df = Cooper(age = 46,weight = 74,distance = 2570.0)
```

## 3<sup>rd</sup> step -- Print the file-header

Print the file-header with the command:
```
fh.printHeader()
```

## 4<sup>th</sup> step -- Define the workout sequence

The workout sequence should be defined according to the runner objective. It can be an **EASY** session just for endurance improvment, and **THRESHDOLD** or **INTERVALS** session for performance improvment, etc.

Four functions are availabel in order to describe a workout: **Warmup**, **SteadyState**, **IntervalsT** and **Cooldown**. The description and procedure to use each one is below depicted.

#### Warmup function

The **Warmup** function is used in the beggining of the training session in order to warm up the body and make it ready to the next efforts. The function uses a distance and two intensities as input. The distance corresponds to the warming up distance to be covered (in meters), and the intensities correspond to an array with the initial and final loads. For the intensities, five values are allowed: **'easy'**, **'marathon'**, **'threashold'**, **'interval'** and **'repetition'**, with one specific pace corresponding to each value.

So, in order to insert a warming up workout, just write:

```
df.Warmup(distance = WARM UP DISTANCE,intensity = WARM UP INTENSITIES)
```

for example:

```
df.Warmup(distance = 1000,intensity = ['easy','marathon'])
```

#### Cooldown function

The **Cooldown** function follows the same principle of the **Warmup** function, and it is used at the end of the workout in order to cool down the body and avoid injuries caused by abrupt stop of an activity.

So, in order to insert a cooling down workout, just write:

```
df.Cooldown(distance = COOL DOWN DISTANCE,intensity = COOL DOWN INTENSITIES)
```

for example:

```
df.Cooldown(distance = 1000,intensity = ['marathon','easy'])
```

#### SteadyState function

The **SteadyState** function is the normal running workout and is implemented according to two variables, distance and intensity, the same as above in case of **Warmup** and **Cooldown**, except that one-sole intensity must be declared.

So, in order to insert a steady state workout, just write:

```
df.SteadyState(distance = STEADY STATE DISTANCE,intensity = STEADY STATE INTENSITY)
```

for example:

```
df.SteadyState(distance = 6800,intensity = ['threshold'])
```

#### IntervalsT function

The **IntervalsT** function is used to implement workouts with high/low intensity periods. It follows the same principle of the **Warmup/Cooldown** function, summed the necessity to declare the number of repetitions for the high/low phases.

So, in order to insert a steady state workout, just write:

```
df.IntervalsT(distance = INTERVALS DISTANCES,intensity = INTERVALS INTENSITY,repetitions = NUMBER OF REPETITIONS)
```

Please note that for intervals it is necessary to input two distances through and 2 x 1 array, the first for the high intensity distance, and the second for the recovery distance, for example:

```
df.IntervalsT(distance = [200,200],intensity = ['repetition','easy'])
```

## 5<sup>th</sup> step -- Close the file

Print the file-closer with the command:
```
fh.Close()
```

## 6<sup>th</sup> step -- Run the code and copy the output

Run the code and copy the output to a **.zwo** file.

The final result should look like this:
```
<workout_file>
<author>Luis H.</author>
<name>ONE-MILE-THRESHOLD</name>
<description>JACK DANIELS -- Training Plan for Half Marathon PHASE III: WEEK 9 | 6.80 T + 0.40 E + 6 x (0.20 R + 0.20 E)</description>
<sportType>run</sportType>
<workout>
<Warmup Duration="1000" PowerLow="0.71018662" PowerHigh="0.80679108" pace="1" />
<SteadyState Duration="6800" Power="0.90339554" pace="1" />
<SteadyState Duration="400" Power="0.71018662" pace="1" />
<IntervalsT Repeat="6" OnDuration="200" OffDuration="200" OnPower="1.14490669" OffPower="0.71018662" pace="1" \>
<Cooldown Duration="1000" PowerLow="0.80679108" PowerHigh="0.71018662" pace="1" />
</workout>
</workout_file>
```
