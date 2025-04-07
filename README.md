import requests
from requests_oauthlib import OAuth1
API_KEY = "msq45c2k9Wc6GIkN0h4ZHFY0w"
API_SECRET = "dIeGCapPTIRN9gSLTghjFJwskb7CDwdjd9hnk3FpWFxeYkPKXL"
ACCESS_TOKEN = "1532435555366998016-lxENkRnyHtRTizAFIRk2hz22aaCdXU"
ACCESS_TOKEN_SECRET = "40lwi4fGU1OYwiuhg19Dop2U4hqpMf1LWWpYLuSAPFWDm"

# OAuth1 authentication
oauth = OAuth1(API_KEY,client_secret=API_SECRET,resource_owner_key=ACCESS_TOKEN,resource_owner_secret=ACCESS_TOKEN_SECRET)
while True:
    print("1 - Post a tweet")
    print("2 - Delete a tweet")
    print("3 - exit ")
    option = int(input("select option : \n"))

    if (option==1):
            # Send POST tweet request
            
            message = input("Enter a tweet mesage : ")
            payload = {"text": message}
            # API endpoint to create tweet
            endpoint = "https://api.twitter.com/2/tweets"
            response = requests.post(endpoint, auth=oauth, json=payload)
    print("Response : ", response.text,"\nCheck your message is deleted from Twitter profile page\n")

        # Send DELETE request
    if (option==2):
        tweet_id = int(input("Enter created tweet ID : "))
                    # API endpoint to delete
        endpoint = f"https://api.twitter.com/2/tweets/{tweet_id}"
        response = requests.delete(endpoint, auth=oauth)
    print("Response : ", response.text,"\nCheck your message is deleted from Twitter Profile page")

            # TO Exit
    if (option==3):
        exit()
            # TO Handle Invalid option
        case
        print("Please select valid Option\n")


        TF.PY-------------------------------------------------------------------------------------------------


from sklearn.feature_extraction.text import TfidfVectorizer 
import pandas as pd 
document_Speech_1 = "The car is driven on the road" 
document_Speech_2 = "The truck is driven on the highway"
corpus = [document_Speech_1, document_Speech_2] 
vectorizer = TfidfVectorizer(stop_words='english') 
X = vectorizer.fit_transform(corpus) 
feature_names = vectorizer.get_feature_names_out() 
df = pd.DataFrame.sparse.from_spmatrix(X, columns=feature_names) 
print(df.head())



        GITHUB.PY--------------------------------------------------------------------------------------------------

        import requests
def get_user_info(username, token):
    url = f"https://api.github.com/users/{username}"
    headers = {"Authorization": f"Bearer {token}"}
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        user_data = response.json()
        print(f"User: {user_data['login']}")
        print(f"Name: {user_data.get('name', 'Not available')}")
        print(f"Followers: {user_data['followers']}")
        print(f"Public Repositories: {user_data['public_repos']}")
    else:
        print(f"Error: {response.status_code}")

# Replace 'User name' with the GitHub username you want to explore
# Replace 'token' with the personal access token you generated
get_user_info('swetha-devaraj', 'ghp_arcrG92jNT1QRJ3xIeUDk63A6S33')


  GITHUB2.PY----------------------------------------------------------------------------------------------------------


  import requests
import pandas as pd

def get_user_repositories(username, token):
    url = f'https://api.github.com/users/{username}/repos'
    headers = {'Authorization': f'token {token}'}
    response = requests.get(url, headers=headers)
    return response.json()

# Replace 'YOUR_USERNAME' and 'YOUR_TOKEN' with your GitHub username and token
repositories = get_user_repositories('SN-API-Testing', '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')

df = pd.DataFrame(repositories)

import matplotlib.pyplot as plt

plt.bar(df['name'], df['stargazers_count'])
plt.xlabel('Repository Name')
plt.ylabel('Number of Stars')
plt.title('GitHub Repository Stars')
plt.xticks(rotation=45, ha='right')
plt.show()



FACEBOOK1.PY------------------------------------------------------------------------------------------------------

import facebook

# Replace 'YOUR_ACCESS_TOKEN' with your actual access token
access_token = 'EAAEbH8tzKQoBO2ZAdaeUQ8aJxOpGCkGkzTI3MydtmgnJLOT4HWPVygwICPEpByiZCmz8L3hvRMhRHZBzYUUvIcAB4bTKT3OQueZBit51ngss4LQZBPwEHlNXIjzJBfhYiJYvN0DNrcUmqJyxvlPZCC4dzqt0kulfoMzbeksx9tdgo43B6jVn07p71DHFxs6GPJsrX3ZCYhEhfWKtA18JqAZBVZA5jQ4ki'

# Create a Graph API object
graph = facebook.GraphAPI(access_token)

# Example: Fetch information about a user
user_info = graph.get_object('122108451014170721')
print("User Info:")
print(user_info)

user_friends = graph.get_connections('122108451014170721', 'friends')
if 'summary' in user_friends:
    frdli = user_friends['summary']
    if 'total_count' in frdli:
        frlist=frdli['total_count']
    print("No.of User's Friends is: ",frlist)
    


FACEBOOK2.PY-----------------------------------------------------------------------------------------------------------------------------

import facebook

access_token = 'EAAEbH8tzKQoBOZCorB8htqUgEF7I3Eh2UmQprkE8OSVpqB1ZCucedcV32ZA5vZBDd67tTMF840d0AZAgQZCcxHnGINgjU0jPQJDUrqG0vx5JetZBGXoL0vPqxOPQZBwoX6ZA931Yt87KaAhh0YBkWA3qZCZBgNrLbxzZBZAKzhD93P3CjZB3pg4rLEV7OTBQydyfm3EE4RSZCJOO1iCaFxmw51LIvbA1vPtgQZDZD'

graph = facebook.GraphAPI(access_token)
page_id='206696835858661'
msg=' '
while True:
    print("1.Publish a Post")
    print("2.Delete a post")
    print("3.Exit")
    ch = int(input("Enter a options:\n"))
    if ch == 1:
        post=input("Enter a post:\n")
        if post==' ':
            print("Post cannot be empty")
        else:
            msg = graph.put_object("me","feed",message=post)
            print("Posted Successfully!")
            print("Your post id is ")
            posts = graph.get_connections(page_id, 'posts')
            if 'data' in posts:
                for post in posts['data']:
                    print(f"Post ID: {post['id']}")
                    msg=str((post['id']))
    elif ch == 2:
        if msg==' ':
            print("It doesn't have Post.")
        else:
            try:
                m=graph.delete_object(msg)
                print("Post successfully deleted!")
            except facebook.GraphAPIError as e:
                print(f"Error: {e}")
    elif ch == 3:
        break
    else:
        print("Invalid options")



