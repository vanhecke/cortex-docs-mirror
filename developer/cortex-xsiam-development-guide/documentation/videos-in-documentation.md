# Videos in documentation

A video can provide a strong addition to the documentation either as a demo video or tutorial. The preferred video format is MP4.

#### Videos stored in GitHub

Because of their size and to keep the main content repository small, large media files are stored in a separate repository.

To add a video file, open a pull request with the video file at [content-assets](https://github.com/demisto/content-assets/pulls) repository. The file should be placed in the directory: `Assets/<PackName>/`.

All videos should be included with absolute URLs. To obtain a URL to a video from GitHub follow the same steps as detailed for [images](images-in-documentation), but use the [content-assets](https://github.com/demisto/content-assets) repository.

Include the video using the HTML `<video>` tag, such as:

```programlisting
<video controls>
    <source src="https://github.com/demisto/content-assets/raw/7982404664dc68c2035b7c701d093ec026628802/Assets/FeedJSON/Json_generic_feed_demo.mp4"
            type="video/mp4"/>
    Sorry, your browser doesn't support embedded videos. You can download the video at: https://github.com/demisto/content-assets/blob/7982404664dc68c2035b7c701d093ec026628802/Assets/FeedJSON/Json_generic_feed_demo.mp4 
</video>
```

{% hint style="info" %}
### Note

GitHub markdown preview does not display the video (it shows the `browser not supported` message). The xsoar.pan.dev site does display the video properly. You can see [an example](https://xsoar.pan.dev/docs/reference/integrations/json-feed#demo-video) video in the JSON Feed integration documentation.
{% endhint %}

#### Large files (over 50MB)

For files larger than 50MB, we require using [git-lfs](https://git-lfs.com/) to add these files to the content repo. See the [GIT LFS Tutorial](https://github.com/git-lfs/git-lfs/wiki/Tutorial) at the GithHub site for more details.

To add a large file:

1. Clone or fork the [content-assets](https://github.com/demisto/content-assets) repository.
2. Verify you have git-lfs installed. See instructions [here](https://github.com/git-lfs/git-lfs/wiki/Installation).
3. Install git-lfs in the repo: `git lfs install`.
4. Copy the video file to the correct directory: `Assets/<PackName>`.
5. Add the video as a tracked file: `git lfs track Assets/<PackName>/<video_file_name>.mp4`.
6. Add the file to git: `git add Assets/<PackName>/<video_file_name>.mp4`.
7. Add the `.gitattributes` file: `git add .gitattributes`.
8. Commit and push using: `git commit` and `git push`.
9. Open a pull request.

#### Videos via external hosting (YouTube)

You can also embed videos from external services such as YouTube via an iframe. From the external service choose to share the video and choose the **Embed** option. Then choose to **Copy** the embed snippet.

Share Dialog

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-97d1e798d2ddb8a0543d3e22900ac7c32c7545e0%2Fbcc746f25b5321527c7bd90feac2f13761eaed595dc437f141db5b0b730726bc.png?alt=media)

Embed Dialog

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-1f57c8735b7e5f20cbf639fd5945fe75211e196b%2F9f398ae8aa5d845da746fe88c87b6d467220733c5e8f4dd4ab4fa9e5499b3638.png?alt=media)

Paste the embed snippet in the README file. Change the `allowfullscreen` option to include `allowfullscreen="true"`. For example:

```programlisting
<iframe width="560" height="315" src="https://www.YouTube.com/embed/s9lRtJltTGI" frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen="true"></iframe>
```
