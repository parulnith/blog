---
toc: true
layout: post
description: Making the most of Google Colab notebooks
comments: true
categories: [Programming, Colaboratory, Jupyter Notebooks]
image: images/2021-05-10-Use Colab more efficiently with these hacks/0.png
show_image: true
show_tags: true
title: "Use Colab more efficiently with these hacks"
---

[Colaboratory](https://colab.research.google.com/notebooks/intro.ipynb), or “Colab” for short, are hosted Jupyter Notebooks by Google, They allow you to write and execute Python code via your browser. It is effortless to spin a Colab since it is directly integrated with your Google account. Colab provides free access to GPUs and TPUs, requires zero-configuration, and makes sharing of code seamless.

Colab has an interesting history. It initially started as an internal tool for data analysis at Google. However, later it was launched publically, and since then, many people have been using this tool to accomplish their machine learning tasks. Many students and people who do not have a GPU rely on colab for the free resources to run their machine learning experiments.

This article compiles some useful tips and hacks that I use to get my work done in Colab. I have tried to list most of the sources where I read them first. Hopefully, these tricks should help you to make the most of your Colab notebooks.

### 1. Using local runtimes 🖥

Typically, Colab provides you with free GPU resources. However, If you have your own GPUs and still want to utilize the Colab UI, there is a way. You can use the Colab UI with a local runtime as follows:

![Alt Text](https://cdn-images-1.medium.com/max/2358/1*6ji2cSekUduGs-pFUH4fFw.png)

This way, you can execute code on your local hardware and access your local file system without leaving the Colab notebook. The [official documentation](https://research.google.com/colaboratory/local-runtimes.html) goes deeper into the way it works.

---

### 2. Scratchpad 📃

Do you end up creating multiple Colab notebooks with names like “untitled 1.ipynb” and “untitled 2.ipynb” etc.? I guess most of us are sail in the same boat in this regard. If that’s the case, then the [Cloud scratchpad notebook](https://colab.research.google.com/notebooks/empty.ipynb) might be for you. The Cloud scratchpad is a special notebook available at the URL — [https://colab.research.google.com/notebooks/empty.ipynb](https://colab.research.google.com/notebooks/empty.ipynb) that is not automatically saved to your drive account. It is great for experimentation or nontrivial work and doesn’t take space in Google drive.

![Alt Text](https://cdn-images-1.medium.com/max/2000/1*zJ5kCgojJOUFAu3jqmYTHw.png)



---


### 3. Open GitHub Jupyter Notebooks directly in Colab 📖

Colab notebooks are designed in a way that they can easily integrate with GitHub. This means you can both load and save Colab notebooks to GitHub, directly. There is a handy way to do that, thanks to [Seungjae Ryan Lee](https://www.endtoend.ai/blog/githubtocolab/).

When you’re on a notebook on GitHub which you want to open in Colab, replace github with githubtocolab in the URL, leaving everything else untouched. This opens the same notebook in Colab.

![Alt Text](https://cdn-images-1.medium.com/max/2412/1*wu-uPw3mSjZRqv815L333w.gif)

---

### 4. Get Notified of completed cell executions 🔔

Colab can notify you of completed executions even if you switch to another tab, window, or application. You can enable it via Tools → Settings → Site → Show desktop notifications (and allow browser notifications once prompted) to check it out.

![Alt Text](https://cdn-images-1.medium.com/max/2076/1*i5apguaDKcITqss1h_ZA3g.jpeg)

Here is a demo of how the notification appears even if you navigate to another tab.

![Alt Text](https://cdn-images-1.medium.com/max/2000/1*sgv8GJBBPlsdnu92qCXUcA.gif)



#### Additional Tip
>  Do you want this same functionality in your Jupyter Notebooks as well ? Well, I have you covered. You can also enable notifications in your **Jupyter notebooks** for cell completion. For details you can read a blog that I wrote on the same topic - 
[Enabling notifications in your Jupyter notebooks for cell completion](https://towardsdatascience.com/enabling-notifications-in-your-jupyter-notebooks-for-cell-completion-68d82b02bbc6)


---


### 5. Search for all notebooks in drive 🔍

Do you want to search for a specific Colab notebook in the drive? Navigate to the Drive search box and add :

    application/vnd.google.colaboratory

This will list all the Colab notebooks in your Google Drive. Additionally, you can also specify the title and ownership of a specific notebook. For instance, if I want to search for a notebook created by me, having ‘Transfer’ in its title, I would mention the following:

![Alt Text](https://cdn-images-1.medium.com/max/2128/1*iYWZvJtGrWkQLdsA0Q27yg.png)


---

### 6. Kaggle Datasets into Google Colab 🏅

If you are on a budget and have exhausted your GPU resources quota on Kaggle, this hack might come as a respite for you. It is possible to download any dataset seamlessly from Kaggle onto your Colab infrastructure. Here is what you need to do:

 - Download your Kaggle API Token :


![Alt Text](https://cdn-images-1.medium.com/max/2000/1*5YNIeB_jg24OlF-Z5i_AYA.jpeg)

On clicking the. ‘Create New API Token’ tab, a kaggle.json file will be generated that contains your API token. Create a folder named **Kaggle** in your Google Drive and store the kaggle.json file in it.

![Alt Text](https://cdn-images-1.medium.com/max/2000/1*dJ0_4MDuwkOYHrU8I_UsfA.png)

 - Mount Drive in Colab Notebook

![Alt Text](https://cdn-images-1.medium.com/max/2000/1*u6CT4f5OiI3HZreF0k1Tqg.png)

 - Provide the config path to `kaggle.json` and change the current working directory

    import os
    os.environ['KAGGLE_CONFIG_DIR'] = "/content/drive/My Drive/Kaggle"
    
    %cd /content/drive/MyDrive/Kaggle

 - Copy the API of the dataset to be downloaded.

For standard datasets, the API can be accessed as follows;

![Alt Text](https://cdn-images-1.medium.com/max/2000/1*_glS_N-A59cjpQNgxeIP2g.png)

###### [Forbes Billionaires 2021 dataset publically available on Kaggle](http://Forbes%20Billionaires%202021%203.0)


For datasets linked to competitions, the API is present under the ‘Data’ tab:

![Alt Text](https://cdn-images-1.medium.com/max/2000/1*65JC4CA097tXAHMCuKr_Dg.png)

##### [IEEE-CIS Fraud Detection competition](http://IEEE-CIS%20Fraud%20Detection)


- Finally, run the following command to download the datasets:
	 
	  !kaggle datasets download -d alexanderbader/forbes-billionaires-2021-30
       #or 
      !kaggle competitions download -c ieee-fraud-detection


![Alt Text](https://cdn-images-1.medium.com/max/2690/1*lSXlKNZJE_U8uEPnKO-UlQ.gif)

---

### 7. Accessing Visual Studio Code(VS Code) on Colab 💻

Do you want to use Colab’s infrastructure without using notebooks? Then this tip might be for you. Thanks to the community's efforts in creating a package called [ColabCode](https://github.com/abhi1thakur/colabcode). It is now possible to run VSCode in Colab. Technically it is accomplished via [Code Server](https://github.com/cdr/code-server) — a [Visual Studio Code](https://code.visualstudio.com/) instance running on a remote server accessible through any web browser. Detailed instructions for installing the package can be found here - https://github.com/abhi1thakur/colabcode.

Here is a quick demo of the process.

![Alt Text](https://cdn-images-1.medium.com/max/2990/1*PKprKU7ZuluaFnHpecODrA.gif)

---

### 8. Data Table extension 🗄

Colab includes an [extension](https://colab.research.google.com/notebooks/data_table.ipynb#scrollTo=JgBtx0xFFv_i) that renders pandas' dataframes into interactive displays that can be filtered, sorted, and explored dynamically. To enable Data table display for Pandas dataframes, type in the following in the notebook cell:

    %load_ext google.colab.data_table

    #To disable the display
    %unload_ext google.colab.data_table

Here is a quick demo of the same: [https://colab.research.google.com/notebooks/data_table.ipyn](https://colab.research.google.com/notebooks/data_table.ipyn)b

![Alt Text](https://cdn-images-1.medium.com/max/2756/1*uaxaUG6PCKpEUIfVoPhuPQ.gif)

---

### 9. Comparing Notebooks 👀

Colab makes it easy to compare two notebooks. Use View > Diff notebooks from the Colab menu or navigate to [https://colab.research.google.com/diff](https://t.co/wu8ce4ngMl?amp=1) and paste the Colab URLs of the notebooks to be compared, in the input boxes at the top.

![Alt Text](https://cdn-images-1.medium.com/max/3448/1*0iKtKyXMXMAfe5-4N5mebg.gif)

---

### Wrap Up

These were some of the Colab tricks that I have found very useful, especially when it comes to training machine learning models on GPUs. Even though Colab notebooks can only run for at most 12 hours, nevertheless, with the hacks shared above, you should be able to make the most out of your session.

