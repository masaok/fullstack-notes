- [Git Submodules](#git-submodules)
  - [Steps to Add Git Submodules](#steps-to-add-git-submodules)
  - [Benefits of Git Submodules](#benefits-of-git-submodules)
  - [Drawbacks of Git Submodules](#drawbacks-of-git-submodules)
  - [Alternatives to Git Submodules](#alternatives-to-git-submodules)
  - [Conclusion](#conclusion)
- [Pushing to a Submodule Requires Updating and Pushing the Parent](#pushing-to-a-submodule-requires-updating-and-pushing-the-parent)
  - [1. **Pushing Changes to the Submodule**](#1-pushing-changes-to-the-submodule)
  - [2. **Updating the Parent Repository**](#2-updating-the-parent-repository)
  - [3. **Pushing the Parent Repository**](#3-pushing-the-parent-repository)
  - [Summary](#summary)

Combining both Frontend and Backend notes using Git submodules.

When you clone this repository, you’ll need to initialize and update the submodules:

```bash
git submodule update --init --recursive
```

## Git Submodules

A **Git submodule** allows you to include one Git repository inside another, essentially linking the two repositories in a way that enables you to keep them separate but connected. This is a more Git-native solution for linking repositories than using symlinks. The submodule is essentially a reference to a specific commit of another repository, and it can be updated independently.

Here’s how to add a Git submodule to a repository:

### Steps to Add Git Submodules

1. **Create the New Repository on GitHub**

   - Start by creating a new empty repository on GitHub.

2. **Clone the New Repository Locally**

   - Clone the new repository:
     ```bash
     git clone https://github.com/your-username/new-repo.git
     cd new-repo
     ```

3. **Add Submodules**

   - To link an existing repository (let’s say `repo1` and `repo2`) to your new repository, you can add them as submodules:

     ```bash
     git submodule add https://github.com/your-username/repo1.git repo1
     git submodule add https://github.com/your-username/repo2.git repo2
     ```

   - This command will add the existing repositories (`repo1` and `repo2`) as submodules, placing them in directories named `repo1` and `repo2` in your new repository.

4. **Initialize and Update the Submodules**

   - After adding submodules, initialize and update them:
     ```bash
     git submodule update --init --recursive
     ```

5. **Commit the Changes**

   - Once the submodules are added, commit the changes in the new repository:
     ```bash
     git add .gitmodules repo1 repo2
     git commit -m "Added repo1 and repo2 as submodules"
     git push origin main
     ```

6. **Manage Submodules**
   - When you clone the new repository later, you’ll need to initialize and update the submodules to retrieve the content:
     ```bash
     git submodule update --init --recursive
     ```

### Benefits of Git Submodules

- **Separation**: Each repository remains independent, and you can manage them separately.
- **Tracking Specific Commits**: You can specify which commit of the submodule you want to use, giving you control over the version of the linked repositories.
- **Efficient Collaboration**: If you’re working on a project that depends on other repositories, submodules allow you to manage dependencies without copying or duplicating code.

### Drawbacks of Git Submodules

- **Complexity**: Managing submodules can be more complex than simply including code or linking repositories.
- **Requires Explicit Updates**: Submodules don’t automatically update when you pull changes in the main repository. You need to explicitly update them.

### Alternatives to Git Submodules

If you don't want to use submodules and want something simpler, here are some other ways to link repositories:

- **Git Subtrees**: A subtree allows you to merge a repository into another without the complexities of submodules. It lets you maintain the history of the linked repository.
- **Monorepos**: You can also consider using a monorepo, where you combine multiple repositories into one larger repository but manage them in separate directories.

### Conclusion

Git submodules are the closest equivalent to soft links between repositories in Git. They allow you to maintain the separation between repositories while linking them together in a manageable way.

## Pushing to a Submodule Requires Updating and Pushing the Parent

If you push changes to a **submodule**, you don’t necessarily need to push the **parent module** immediately, but you will likely want to do so to ensure the parent module points to the updated commit in the submodule. Here’s how it works:

### 1. **Pushing Changes to the Submodule**

- When you make changes in a submodule and push those changes to the submodule's own repository, it only affects that specific submodule repository.
- However, the parent repository keeps a **reference to the specific commit** of the submodule that it’s tracking.

### 2. **Updating the Parent Repository**

- After updating and pushing changes in the submodule, the parent repository will still be referencing the old commit ID of the submodule. To update this reference:
  - Go to the parent repository.
  - Run `git add` on the submodule directory to register the new commit reference.
  - Commit the change in the parent repository, which now points to the updated submodule commit.

```bash
git add path/to/submodule
git commit -m "Updated submodule to latest commit"
```

### 3. **Pushing the Parent Repository**

- After committing the updated submodule reference, push the changes in the parent repository. This step ensures that when others pull the parent repository, they’ll see the latest commit of the submodule.

```bash
git push origin main
```

### Summary

If you make changes to a submodule:

1. Push those changes to the submodule's own repository.
2. Update the submodule reference in the parent repository and commit.
3. Push the parent repository to share the updated submodule reference with others.

If you skip updating and pushing the parent repository, others will not see the updated submodule commit when they pull the parent repository.
