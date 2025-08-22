Optimizer Journey & Reflections

I started with the classics—Momentum, Nesterov, AdaGrad—and then moved through the modern hitters: RMSProp, Adam, Nadam, and AdamW.

What stood out is exactly what Geoff Hinton hinted years back: RMSProp just works.
Why? Because it adapts learning rates per-parameter like AdaGrad, but instead of decaying into oblivion, it keeps a running average of squared gradients. That balance—between stability and adaptability—let it consistently cut through plateaus and converge faster in my experiments.

Adam and AdamW were strong contenders, but they often felt like “too clever” optimizers: fast convergence, yes, but sometimes poorer generalization and overfitting. RMSProp gave me the most trustworthy training curves. Nadam didn’t give me much extra beyond Adam—it just complicated things.

Model Fixes That Paid Off

Early Stopping with restore_best_weights → protected against overfitting spikes.

Gradual narrowing (“triangle technique”) in hidden layers → way better than a flat slab, likely because it forces feature compression.

Resetting to clean initial weights before optimizer swaps → avoided false comparisons between optimizers.

Together, these gave me a model that not only trained smoothly but also generalized much better.

Why the Cost Was High

The training cost (loss) stayed higher than I expected. The main culprit? L2 regularization.

L2 penalizes large weights, which is great for keeping the model simpler and avoiding overfitting—but it inflates the loss value itself because it literally adds a penalty term on top of the data loss.
So the higher cost didn’t mean the model was bad—it meant the regularization was doing its job, making the network “pay rent” for complexity.

Takeaway

After cycling through the entire zoo of optimizers, I see why RMSProp still holds a special place: it’s simple, elegant, and robust—sometimes, the “old” tricks still win when measured by clarity, stability, and generalization.
