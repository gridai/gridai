# Github login

Interactive Sessions automatically login into Github for you. You can clone any repositories into a Session using the [HTTPS cloning method](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository#cloning-a-repository-using-the-command-line) \(SSH will not work\).

![Cloning a private repository into a Grid Interactive Session.](../../.gitbook/assets/git_clone_private_repo.gif)

## Signed up with Github

If you signed up to Grid with Github, you'll already be logged into your Github account when an interactive Session starts.

![](../../.gitbook/assets/image%20%28147%29.png)

## Signed up with Google

If you signed up to Grid with Google, you'll have to link a Github account under **Settings** &gt; **Integrations**.

![](../../.gitbook/assets/image%20%28121%29.png)

## Access Private Github Repos

By default you can only access public Github repositories on Grid. To grant access to your private code navigate to Settings &gt; Integrations &gt; Grant access.

![](../../.gitbook/assets/github.gif)

## About authorization

When you grant access to private repositories in Github, the organizations that you have granted private access to will appear in [https://github.com/settings/applications](https://github.com/settings/applications) .  When you want to use a script from a private repository in Grid, make sure that the organization shows up in the Applications section of Github settings

![Settings-&amp;gt;Applications](../../.gitbook/assets/screen-shot-2021-05-20-at-4.16.45-pm.png)

Click on the Grid AI organization to see permissions.

![](../../.gitbook/assets/screen-shot-2021-05-20-at-5.00.49-pm.png)

Make sure that Organization access above shows that permissions are granted to the repositories you have\(this example is showing xyz\). If Organization access is not requested, you will not be able to use scripts from the private repositories.

## About private code

Grid does not save your code, look at it or compromise its privacy in any way.

When receiving support, you will not have to share any code to help debug. If you choose to share code, make sure you have the rights to and share non-critical parts of the code.





