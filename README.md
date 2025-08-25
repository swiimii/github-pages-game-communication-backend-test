# Communicate To Players with Github Pages

Want to communicate game updates to your players, but don't want to host a dynamic backend for your relatively simple Unity game? Just make a Github Pages blog!

Jokes aside, I created this repo to answer my simple question: will anything stop me from using Github pages for my backend?

Traditionally, Github Pages is not intended to be a backend server. It doesn't support the features necessary to host game lobbies, or anything fancy like that. However you can still use it to transmit information to your game!

Enter: *using a frontend as your backend!* With a simply GET request, you too can display the contents of my index.html in your Unity game! Or *your* index.html, if you feel like it!

Simply add the below monobehavior to your project, drop it onto a game object, and boom - you'll see the contents of my web page in *your* Unity console!

While this isn't the *best* way of creating a game backend, it's one which you can use if you're low on time or resources. Remember that Github Pages is a free service, so no fees for hosting your cool player-communication system! Simply push your latest message to your repository, and update your players in real time!

I'm sure this isn't the most performant nor the most elegant way of handling this sort of system, but it's one that's zero-cost and which requires little time commitment, which is a fantastic combo for an indie dev like myself!

```C#
using System.Collections;
using UnityEngine;
using UnityEngine.Networking;

public class TestPing : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        StartCoroutine(GetMessage());
    }

    public IEnumerator GetMessage()
    {
        var response = UnityWebRequest.Get("https://www.sam-scherer.com/github-pages-game-communication-backend-test/");
        response.SendWebRequest();

        while( !(response.result != UnityWebRequest.Result.InProgress) )
        {
            yield return null;
        }

        Debug.Log("Done!");
        Debug.Log(response.downloadHandler.text);
    }
}

```