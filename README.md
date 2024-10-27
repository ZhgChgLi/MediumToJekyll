![ZMediumToJekyll](https://user-images.githubusercontent.com/33706588/225700695-fcbbdd87-2eaf-4629-bbe9-3ab1d9f7f5e6.jpg)

[![Automatic build](../../actions/workflows/pages-deploy.yml/badge.svg)](../../actions/workflows/pages-deploy.yml)
[![pages-build-deployment](../../actions/workflows/pages/pages-build-deployment/badge.svg)](../../actions/workflows/pages/pages-build-deployment)
[![ZMediumToMarkdown](https://github.com/ZhgChgLi/zhgchgli.github.io/actions/workflows/ZMediumToMarkdown.yml/badge.svg)](https://github.com/ZhgChgLi/zhgchgli.github.io/actions/workflows/ZMediumToMarkdown.yml)


This tool can help you move your Medium posts to a Jekyll blog and keep them in sync in the future.

**One-time setting, Lifetime enjoying❤️**

It will automatically download your posts from Medium, convert them to Markdown, and upload them to your repository, check out [my blog](https://github.com/ZhgChgLi/zhgchgli.github.io/) for online demo [zhgchg.li](https://zhgchg.li).

Powered by [ZMediumToMarkdown](https://github.com/ZhgChgLi/ZMediumToMarkdown).

If you only want to create a backup or auto-sync of your Medium posts, you can use the GitHub Action directly by following the instructions in this [Wiki](https://github.com/ZhgChgLi/ZMediumToMarkdown/wiki/How-to-use-Github-Action-as-your-free-&-no-code-Medium-Posts-backup-service).

# Buy me a coffee ❤️❤️❤️

<a href="https://www.buymeacoffee.com/zhgchgli" target="_blank"><img width="545" alt="bmc-button" src="https://github.com/user-attachments/assets/5983bfc9-27fd-49e0-a7f4-eb07657c6e31"></a>

[**If this project has helped you, feel free to sponsor me a cup of coffee, thank you.**](https://www.buymeacoffee.com/zhgchgli)

----

## Setup

- You can follow along with each step of this process by watching the following [video tutorial](https://www.youtube.com/watch?v=qsnZKFL3vks)

1. Click the green button `Use this template` located above and select `Create a new repository`.
2. Repo Owner could be an organization or username
2. Enter the **Repository Name**, which usually uses your **GitHub Username/Organization Name** and ends with `.github.io`, for example, my organization name is `zhgchgli` than it'll be `zhgchgli.github.io`.
3. Select the `public` repository option, and then click on `Create repository from template`.
4. Grant access to GitHub Actions by going to the `Settings` tab in your GitHub repository, selecting `Actions` -> `General`, and finding the `Workflow permissions section`, then, select `Read and write permissions`, and click on `Save` to save the changes.

*If you choose a different Repository Name, the GitHub page will be `https://username.github.io/Repository Name` instead of `https://username.github.io/`, and you will need to fill in the `baseurl` field in `_config.yml` with your Repository Name.

*If you are using an organization and cannot enable `Read and Write permissions` in the repository settings, please refer to the organization settings page and enable it there.

### First-time run

1. Please refer to the configuration information in the section below and make sure to specify your Medium username in the `_zmediumtomarkdown.yml` file.
2. ⌛️ Please wait for the `Automatic Build` and `pages-build-deployment` gitHub actions to finish before making any further changes.
3. Then, you can manually run the ZMediumToMarkdown GitHub action by going to the `Actions` tab in your GitHub repository, selecting the `ZMediumToMarkdown` action, clicking on the `Run workflow` button, and selecting the `main` branch.
4. ⌛️ Please wait for the action to download and convert all Medium posts from the specified username, and commit the posts to your repository.
5. ⌛️ Please wait for the `Automatic Build` and `pages-build-deployment` actions will also need to finish before making any further changes, and that they will start automatically once the ZMediumToMarkdown action has completed.
6. Go to the `Settings` section of your GitHub repository and select `Pages`, In the `Branch` field, select `gh-pages`, and leave `/(root)` selected as the default. Click `Save`, you can also find the URL for your GitHub page at the top of the page.
7. ⌛️ Please wait the `Pages build and deployment` action to finish.
8.  🎉 After all actions are completed, you can visit your xxx.github.io page to verify that the results are correct. Congratulations! 🎉

*To avoid expected Git conflicts or unexpected errors, please follow the steps carefully and in order, and be patient while waiting for each action to complete. 

*Note that the first time running may take longer.

*If you open the URL and notice that something is wrong, such as the web style being missing, please ensure that your configuration in the `_config.yml` file is correct.

***Please refer to the 'Things to Know' and 'Troubleshooting' sections below for more information.**

## Configuration

### Site Setting
#### _zmediumtomarkdown.yml
```
medium_username: # Enter your username on Medium.com
```

Please specify your Medium username for automatic download and syncing of your posts.

#### Supports Paywall posts
[ZMediumToMarkdown](https://github.com/ZhgChgLi/ZMediumToMarkdown) requires `uid` and `sid` cookies to access paywalled posts on Medium.

If you don’t provide valid Medium Member cookies, you will receive this warning message while downloading a Medium post if the post is behind a paywall:
> This post is behind Medium's paywall. You must provide valid Medium Member login cookies to download the full post.

You can obtain `uid` and `sid` cookies from Medium by following these steps:
1. Log in to a valid Medium Member account.
2. Right-click anywhere on the Medium webpage.
3. Select "Inspect" to open the Developer Tools.
4. Navigate to the "Application" tab and locate the `sid` and `uid` values under "Cookies."

![ZhgChgLi-2024-08-11_22-30-03](https://github.com/user-attachments/assets/35229d1d-501a-4ecf-8f3e-592a02416bb1)

##### Add `sid` and `uid`  to repo Secret

![image](https://github.com/user-attachments/assets/53d5af86-dff1-4676-892d-cb3f93329c48)

Settings -> Secrets and variables -> Actions -> Repository secrets -> New repository secret

![image](https://github.com/user-attachments/assets/6e37040b-20a7-4878-a37c-4596fe96144d)

1.
- Name: `MEDIUM_COOKIE_SID`
- Secret: Your `sid` value
2.
- Name: `MEDIUM_COOKIE_UID`
- Secret: Your `uid` value

##### Change Github Action Command

Go To ZMediumToMarkdown.yml Action

![image](https://github.com/user-attachments/assets/3720d6f6-6510-4ef9-8278-b7da9585d819)

Change to command to:

```
--cookie_uid ${{ secrets.MEDIUM_COOKIE_UID }} --cookie_sid ${{ secrets.MEDIUM_COOKIE_SID }} -j ${{ steps.yaml-data.outputs.data }}
```

![image](https://github.com/user-attachments/assets/b3fa9a04-7c4e-4518-8194-ca7ec7f6a5ae)

- Commit & Save
- Done!

**!!!! Ensure that cookie information is stored in repository secrets. Do not expose cookies directly in the action YAML. !!!!**

#### _config.yml & jekyll setting

For more information, please refer to [jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/) or [jekyllrb](https://jekyllrb.com).

### Github Action
#### ZMediumToMarkdown

You can configure the time interval for syncing in `./.github/workflows/ZMediumToMarkdown.yml`.

The default time interval for syncing is once per day.

You can also manually run the ZMediumToMarkdown action by going to the `Actions` tab in your GitHub repository, selecting the `ZMediumToMarkdown` action, clicking on the `Run workflow` button, and selecting the `main` branch.

## Disclaimer

All content downloaded using ZMediumToMarkdown, including but not limited to articles, images, and videos, are subject to copyright laws and belong to their respective owners. ZMediumToMarkdown does not claim ownership of any content downloaded using this tool.

Downloading and using copyrighted content without the owner's permission may be illegal and may result in legal action. ZMediumToMarkdown does not condone or support copyright infringement and will not be held responsible for any misuse of this tool.

Users of ZMediumToMarkdown are solely responsible for ensuring that they have the necessary permissions and rights to download and use any content obtained using this tool. ZMediumToMarkdown is not responsible for any legal issues that may arise from the misuse of this tool.

By using ZMediumToMarkdown, users acknowledge and agree to comply with all applicable copyright laws and regulations.

## Troubleshooting
### If you are facing Run ZMediumToMarkdown Automatic Bot Failed ❌
```
remote: Write access to repository not granted.
fatal: unable to access 'https://github.com/zhgtest/test-init/': The requested URL returned error: 403
Error: Invalid status code: 128
    at ChildProcess.<anonymous> (/home/runner/work/_actions/stefanzweifel/git-auto-commit-action/v4/index.js:17:19)
    at ChildProcess.emit (node:events:513:28)
    at maybeClose (node:internal/child_process:1100:16)
    at Process.ChildProcess._handle.onexit (node:internal/child_process:304:5) {
  code: 128
}

Error: Invalid status code: 128
    at ChildProcess.<anonymous> (/home/runner/work/_actions/stefanzweifel/git-auto-commit-action/v4/index.js:17:19)
    at ChildProcess.emit (node:events:513:28)
    at maybeClose (node:internal/child_process:1100:16)
    at Process.ChildProcess._handle.onexit (node:internal/child_process:304:5)
```

**Please follow steps below to change workflow permission and retry running github action:**

Settings -> Actions -> General -> Workflow Permissions -> Read and write permissions -> ✅

![1_1ZHF9CIOMV8S12Xw2P4B8g](https://github.com/ZhgChgLi/ZReviewTender-deploy-with-github-action/assets/33706588/b2b04098-aff3-4d37-98cb-f04971e7bf1d.png)


### My GitHub page keeps presenting a 404 error or doesn't update with the latest posts.
- Please make sure you have followed the setup steps above in order.
- Wait for all GitHub actions to finish, including the `Pages build and deployment` and `Automatic Build` actions, you can check the progress on the `Actions` tab.
- Make sure you have the correct settings selected in `Settings -> Pages`.

## Things to know
- The `ZMediumToMarkdown` GitHub Action for syncing Medium posts will automatically run every day by default, and you can also manually trigger it on the GitHub Actions page or adjust the sync frequency as needed.
- **Every commit and post change will trigger the `Automatic Build` & `Pages build and deployment` action. Please wait for this action to finish before checking the final result.**
- You can create your own Markdown posts in the `_posts` directory by naming the file as `YYYY-MM-DD-POSTNAME` and recommend using lowercase file names.
- You can include images and other resources in the `/assets` directory.
- Also, if you would like to remove the ZMediumToMarkdown watermark located at the bottom of the post, you may do so. I don't mind.
- You can edit the Ruby file at `tools/optimize_markdown.rb` and uncomment lines `10-12`. This will automatically remove the ZMediumToMarkdown watermark at the end of all posts during Jekyll build time.
- Since ZMediumToMarkdown is not an official tool and Medium does not provide a public API for it, I cannot guarantee that the parser target will not change in the future. However, I have tried to test it for as many cases as possible. If you encounter any rendering errors or Jekyll build errors, please feel free to create an issue and I will fix them as soon as possible.

## Sites That Use ZMediumToJekyll
- [https://zhgchg.li](https://zhgchg.li)

You can add your site to this list by creating a pull request. 😝

## About
- [ZhgChg.Li](https://zhgchg.li/)
- [ZhgChgLi's Medium](https://blog.zhgchg.li/)

## Other works
### Swift Libraries
- [ZMarkupParser](https://github.com/ZhgChgLi/ZMarkupParser) is a pure-Swift library that helps you to convert HTML strings to NSAttributedString with customized style and tags.
- [ZPlayerCacher](https://github.com/ZhgChgLi/ZPlayerCacher) is a lightweight implementation of the AVAssetResourceLoaderDelegate protocol that enables AVPlayerItem to support caching streaming files.
- [ZNSTextAttachment](https://github.com/ZhgChgLi/ZNSTextAttachment) enables NSTextAttachment to download images from remote URLs, support both UITextView and UILabel.

### Integration Tools
- [ZReviewTender](https://github.com/ZhgChgLi/ZReviewTender) is a tool for fetching app reviews from the App Store and Google Play Console and integrating them into your workflow.
- [ZMediumToMarkdown](https://github.com/ZhgChgLi/ZMediumToMarkdown) is a powerful tool that allows you to effortlessly download and convert your Medium posts to Markdown format.
- [linkyee](https://github.com/ZhgChgLi/linkyee) is a fully customized, open-source LinkTree alternative deployed directly on GitHub Pages.

# Donate

[![Buy Me A Coffe](https://img.buymeacoffee.com/button-api/?text=Buy%20me%20a%20beer!&emoji=%F0%9F%8D%BA&slug=zhgchgli&button_colour=FFDD00&font_colour=000000&font_family=Bree&outline_colour=000000&coffee_colour=ffffff)](https://www.buymeacoffee.com/zhgchgli)

If you find this library helpful, please consider starring the repo or recommending it to your friends.

Feel free to open an issue or submit a fix/contribution via pull request. :)
