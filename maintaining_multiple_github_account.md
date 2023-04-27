# GitHub Multiple account

### Why do we need multiple account?

Usually every developer will have their own GitHub account used for own development purposes, and an additional account for office use, this can be in GitHub or BitBucket or anything similar.

### What is the problem we are trying to solve here?

The problem is basically regarding setting up accounts.
The problem is specific to having multiple gitHub accounts and maintaining them locally from a CLI. In a nutshell, the system basically get confused on which remote repository to reach when we perform any git operation.
Hence, we want to have a configuration to redirect all the git actions to the correct remote repository.

### What's the solution?

The solution is simple to have different private-public key generated and used for different accounts and individual repositories using the correct the SSH key to connect to different accounts.

### How to do it?

The details about how to do the changes can be found here:

1. <https://www.freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/>
2. <https://devconnected.com/how-to-change-git-remote-origin/#:~:text=In%20order%20to%20change%20the,remote%20URL%20to%20be%20changed.>

After doing the above we need to make sure that all our git repos are pointing to the correct remote repository. For example here: i am pointing my personal repository to the correct github repo.  git remote set-url origin **git@github.com_mine**:SourabhKr/myNotes.git
