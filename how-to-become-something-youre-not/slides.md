---
theme: default
background: https://images.pexels.com/photos/4021775/pexels-photo-4021775.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2
# use UnoCSS 
css: unocss
---
# How I became a part time (unpaid) dermatologist
## Hasib Ahmed

<!--
Some notes
-->

---
transition: slide-left
---
# Have you ever wanted to become something you're not?

- 🥼 **Doctor**
- 📈 **Stock trader**
- 👩🏼‍🚀 **Astronaut***

With code & a magic thing called ✨**Machine Learning**✨ you can! You can even do it part time, just like how I became a part time (unpaid) dermatologist 🔬

<div v-click>
<img class="h-40 rounded shadow" src="img/derma1.png"/>
</div>
<div v-click>*probably can't be an astronaut with just code</div>

<!--
I wanted to be a super secret spy when I was younger, the dream is still there

Portrait of me
lets demistify ML
-->

---
transition: slide-down
---

# What is Machine Learning?
<div v-click>
<img class="h-100" src="https://theclickhub.com/wp-content/uploads/2019/08/Blog-30-Skynet.jpg"/>
</div>

<!--
This is the general conception of what ML is
Scary, killer robots, taking over our lives
-->

---
transition: slide-up
---

# Reality
<div v-click>
<img class="h-100" src="https://media1.giphy.com/media/fkJO2IcWJhiht7jjJo/giphy.gif?cid=ecf05e47nuwcdve4pcr2obel4ytns5bmi6cf2cnnk6ote572&rid=giphy.gif&ct=g"/>
</div>

<!--
The killer robots aren't so scary now right?
-->

---
transition: fade-out
---

# What is Machine Learning?

<img src="img/ML-definition.png"/>

<div v-click>
<br>
We teach machines to guess what things are, or will, be based on lots and lots of data
<br>
</div>

<div v-after>
<img class="h-40" src="https://media3.giphy.com/media/SY2j8eBZjSPqv7Ggxt/giphy.gif?cid=ecf05e4760rp366iyoi5v29n3wvltqu3vof0c7szkd59nr9o&rid=giphy.gif&ct=g"/>
</div>

---
transition: slide-left
---

# How do machines learn? 🧠💻

The machine or algorithm can understand whatever we tell it to understand. We pick out features, which is known as feature engineering, to help the algorithm to figure out what a piece of data is. A piece of data could be numbers, images, video, etc

<div v-click>
Common example is classifying cats and dogs
</div>
<div v-click>
<img class="h-80 rounded shadow" src="img/cats-dogs.png"/>
</div>

<!--
we would tell the algorithm what is a cat, what is a dog, and what we think differentiates them (pointy ears, the way they sit/stand etc)

now we've gone over the core concepts

-->

---
transition: slide-left
---

# How & why I become a part time Dermatologist

<div v-click>
A family member was  diagnosed with Alopecia areata which is a disease that happens when the immune system attacks hair follicles and causes hair loss.
</div>
<br>
<div v-click>
What serious skin conditions are out there?
</div>
<div v-click>
<ul>
<li><b>Melanoma</b></li>
<li>Benign keratosis</li>
<li>Melanocytic nevi</li>
<li>Basal cell carcinoma</li>
<li>Actinic keratoses</li>
<li>Vascular lesions</li>
<li>Dermatofibroma</li>
</ul>
</div>

<!--
& it got me thinking

One of the most serious is something called Melanoma. Now I know what I need, it's time to find some data on it
-->

---
transition: slide-left
---

# Now I need data & lots of it
<div v-click>
HAM10000 dataset: a large collection of multi-source dermatoscopic images of common pigmented skin lesions
</div>

<div v-click>
10, 000 images 🤔
    <img class="h-100" src="https://media2.giphy.com/media/S4AVBFpmuV16pbpwb9/giphy.gif?cid=ecf05e47hpuf2s541b0zw1ftc11ws1n36sl3a8vbhsth2h2q&rid=giphy.gif&ct=g"/>
</div>

<!--
- after looking through the interwebs I came across a gem
- great, now I have data... now what? I can't go through 10k images by hand
-->

---
transition: fade-out
---

# Explore the dataset, with the power of code
<div v-click>
```python
// Categories of the diferent diseases
lesion_type_dict = {
    'nv': 'Melanocytic nevi',
    'mel': 'Melanoma',
    'bkl': 'Benign keratosis ',
    'bcc': 'Basal cell carcinoma',
    'akiec': 'Actinic keratoses',
    'vasc': 'Vascular lesions',
    'df': 'Dermatofibroma'
}
```
<img class="h-50" src="img/skin-lesion-df1.png"/>
</div>

<!--
some code to translate the skin lesion labels to something human readable rather than the dx acronyms
-->

---
transition: fade-out
---

# Explore the dataset, with the power of code

<div v-click>
```python
df.lesion.value_counts()
```
<img class="h-50" src="img/df-lesions.png"/>
</div>
<div v-click>

Something doesn't look right
</div>
<div v-after>
<img class="h-30" src="https://media2.giphy.com/media/TwYP72KtO8YQQ4SNgz/giphy.gif?cid=ecf05e47ekvm0tb436exk8usipvotsci453e3ypp1znoxmh3&rid=giphy.gif&ct=g"/>
</div>

<!--
what make up of images do I have in my dataset
Definitely showing more of one data point, or skin lesion
-->

---
transition: slide-left
---

# Explore the dataset, with the power of code

<div v-click>
Let's visualise that data
```python
fig, ax1 = plt.subplots(1, 1, figsize = (10, 5))
sns.countplot(y = 'lesion', data = df, hue = "lesion", ax = ax1)
```
<img class="h-50" src="img/df-infographic.png"/>
</div>
<div v-click>
Suspicions confirmed 🫡
</div>
<div v-after>
<img class="h-30" src="https://media4.giphy.com/media/puOukoEvH4uAw/giphy.gif?cid=ecf05e47ekvm0tb436exk8usipvotsci453e3ypp1znoxmh3&rid=giphy.gif&ct=g"/>
</div>
<!--
if data wasn't enough, a graph on top always is
we can see a massive imbalance, this can add to data biases and will skew our results. if ML model guesses brown 70% it'll probably be right for my dataset, but not general application
We can fix this with data augmentation when we train the model
-->

---
transition: fade-out
---

# Now I need a machine learning algorithm to use

<div v-click>
My requirements:
<ul>
    <li>Lightweight for a mobile application</li>
    <li>Ideally pretrained to save me some time & additional work</li>
    <li>A cool name</li>
</ul>
</div>
<div v-click>
Pretrained refers to a machine learning model created by someone else and trained on a large dataset to solve a similar problem.
</div>
<div v-click>
<img class="h65" src="https://media1.giphy.com/media/5wWf7HapUvpOumiXZRK/giphy.gif?cid=ecf05e478dmawwjncmkmcrsujq64nt99oj1m1qhjxzxun9ee&rid=giphy.gif&ct=g"/>
</div>


<!--
now I've explored the data, it's time to pick a machine learning algorithm.
similar problem = image classification
taking what it knows and adding to it
went with MobileNet, since intention was for mobile application & it's trained for general purpose image clasification
-->
