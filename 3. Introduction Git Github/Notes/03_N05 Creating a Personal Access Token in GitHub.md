# Creating a Personal Access Token in GitHub
Personal access tokens are used in place of your GitHub password at the command-line. To use a personal access token, you must first create one. The following is a step-by-step guide on how to create a personal access token in GitHub which will be used in the next lab, 
[Qwiklabs Assessment: Introduction to GitHub](https://www.coursera.org/learn/introduction-git-github/gradedLti/E5MAI/qwiklabs-assessment-introduction-to-github)
. 

<br>

## Steps to creating a personal access token in GitHub

1. Log into your GitHub account with your username and password.

2. In the upper right hand corner click on your profile picture. 

![8Q7jQI_qRg2TdABAEiPfGw_a255fee890664af290776e778fc19ff1_image](https://github.com/kemda2/Google-Courses/assets/19648132/2422ed1b-8599-484d-b9bb-01740b2f1207)

3. Use the drop-down menu, and click on Settings.

![8Q7jQI_qRg2TdABAEiPfGw_a255fee8906](https://github.com/kemda2/Google-Courses/assets/19648132/2ef901ca-69d8-4da6-9ee5-e1c758223949)

4. On the left sidebar, click on Developer Settings. It looks like this:

![Ekran görüntüsü 2024-02-01 131953](https://github.com/kemda2/Google-Courses/assets/19648132/7e928538-dedb-4174-8a7e-863c7563b747)

5. On the left sidebar, click on Personal access tokens. Choose tokens (classic).

![Ekran görüntüsü 2024-02-01 132047](https://github.com/kemda2/Google-Courses/assets/19648132/5b99c67e-a5e5-4b1f-963c-7c2a9d6bca2f)

6. Click Generate new token. Choose Generate new token (classic).

![Ekran görüntüsü 2024-02-01 132128](https://github.com/kemda2/Google-Courses/assets/19648132/685f691e-00fb-49e3-a463-ae885dab6bd6)

7. In the “Note” field, give your token a name. 

8. Set when you want your token to expire.

9. Select the scopes you want to grant this token. For the lab that follows make sure you select repo so that you can access repositories from the command-line. 

![Ekran görüntüsü 2024-02-01 132226](https://github.com/kemda2/Google-Courses/assets/19648132/e1a7155a-e610-4828-942b-6c4eda895298)

10. Click Generate token.

11. Copy your new token to your clipboard. You may want to paste it in a document or note that you will delete after you have completed the lab. You will not be able to see the token again. 

12. Finally, when you go to login to your GitHub account at the command-line use your GitHub username and the token you just generated for your password. 

<br>
<br>

Here is the 
[official documentation](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
 for creating personal access tokens from GitHub. 