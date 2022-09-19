# Back of the Envelope Estimation

> This is a summary of Chapter 2 of [System Design Interview Volume 1](https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF/).

Bytes:
```
----- x 0.001 ---> 
KB, MB, GB, TB, PB
<---- x 1000 -----
```

Seconds:
```
--------- x 0.001 -------> 
nano, micro, mili, seconds
<-------- x 1000 ---------
```


| Availability | Approx. Down time per year |
| ------------ | -------------------------- |
| 99%          | 4 days                     |
| 99.9%        | 9 hours                    |
| 99.99%       | 1 hour                     |
| 99.999%      | 5 minutes                  |
| 99.9999%     | .5 minute                  |

1 day = 86,400 seconds =~ 100K seconds

Peak QPS = 2 * average QPS

## Example:
Given:
- 300M MAU
- 50% users use daily
- Average 2 tweets/day
- 10% of tweets contain media
- Data is stored for 5 years

**QPS**: 300M users x 0.5 x 2 tweets per day per user / 100K seconds per day =~ 3000 tweets per second

**Storage**:  
Suppose average media size is 1MB

150M users per day x 2 tweets per day per user x 1MB per tweet x 10% = 30TB per day.  

For 5 years --> 30TB per day x 5 years x 365 day per year =  ~55PB.


