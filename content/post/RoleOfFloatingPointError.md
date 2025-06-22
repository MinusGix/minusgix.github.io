+++
date = '2025-06-19T21:34:26-04:00'
draft = true
title = 'RoleOfFloatingPointError'
tags = ["Floating Point", "Machine Learning"]
categories = ["Floating Point", "Machine Learning"]
math = true
+++

# What Error?

## The Benefits of Floating Point Error

One benefit that has been observed is that floating point error acts as an implicit regularizer. Similar to injecting (predictable) noise into a model's weights, floating point error encourages some degree of imprecise dependence on the input of the previous layer.
(TODO: there was a paper on this, cite it)

## The Costs
But, does floating point error harm learning?

Gradients presume a smooth space to optimize over, but floating point numbers are clearly discrete. While they can represent quite a few values, small tweaks are not necessarily possible.  
While this would not be a problem if this could be represented in the gradient—however that is supposed to work!—it is clearly not.  

An obvious case of this would be a neuron that wants to be 0.X, but 0.X is not a valid floating point number. It is bracketed by 0.Y99999 and 0.Z00001. These may very well demarcate different regions of processing, and so it tries repeatedly pushing itself to a better value (0.X) but all it can reach is one of the two brackets.  
You can effectively think of this as a weaker form of holding a neuron constant in a neural network and refusing gradients updating it. All they can do is adapt around it. However, importantly, it is still being affected and included in gradients. I think this could cause pathologies, because you're effectively calculating *as if* you can update it as part of your adjustment, but you can't. I should construct a test case to demonstrate this if at all possible.  
As an illustrative metaphor, if you are devising a plan that relies on your ability to place a brick in a specific spot but you can only place it at a meter on either side, well, your building may not work out. Thus I'm curious if this messes with the learning process, where the pressure is enough in many locations to get around it, but that too much 'focus' is spent on parts of the model that struggle to learn because they can't be tuned precisely enough. But the gradients effectively insist that they 'can'.

Theoretically, I think this could be even worse of a problem than it sounds. As you scale, you're given more neurons to work around this, but eventually you may get stuck repeatedly. Gears faltering as they are unable to really update in the direction that is optimal, more and more as time goes on, turning into getting stuck in the optimizer. This would be plateaued validation loss, which might resolve with much further training but may seem odd in how stuck it is.

However, this could be a red herring and not really a problem. Float32 is a rather large space, and the state space grows quite a lot. (Not sure if exponentially, because two neurons aren't varying independently of each other, but still quite a lot.)