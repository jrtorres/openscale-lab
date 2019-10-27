# Fairness, Drift and Explainability

## Getting Super Powers

Becoming a super hero is a fairly straight forward process:

```
$ give me super-powers
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

```
// Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```

The “drift” is defined as potential drop in model accuracy from input data. Watson OpenScale can detect when models in production struggle to correctly predict the intended outcomes.

Our approach does not rely on additional feedback data from production. Watson OpenScale can automatically predict a specific scenario where predictions may turn out to be inaccurate. For example, let’s say Watson OpenScale has analyzed the model training data and determined that the credit risk prediction for younger demographics is less accurate than for other demographics. In this case, Watson OpenScale can identify how a sudden influx of applications from the younger demographic is likely to affect overall model accuracy, and even see if this drop in accuracy is correlated with business performance indicators.![Detect drops in accuracy with Watson OpenScale](https://miro.medium.com/max/60/1*DFmoN0yLVhxb4ftFqfTrzA.png?q=20)  


