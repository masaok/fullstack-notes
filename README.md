Combining both Frontend and Backend notes using Git submodules.

When you clone this repository, you’ll need to initialize and update the submodules:

```bash
git submodule update --init --recursive
```

### Git Submodules

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
