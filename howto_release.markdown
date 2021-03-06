# Checklist For Publishing a New Release

To release version x.y.z:

- Update release notes
- bump version of peer dependency *AND* devDependency for traverson in package.json to latest
- bump version in package.json to x.y.z
- bump version in package-lock.json to x.y.z
- npm install
- `npm run build` (to create a fresh browser build, also make sure all tests pass etc.)
- `git commit -am"release x.y.z" && git push`
- `npm publish`
- `git add -f browser/dist/traverson-hal.*` (to add the build artifacts to the release branch)
- `git commit -m"add build artifacts for release"`
- `git push origin release-x.y.z`
- [create a new release on github](https://github.com/traverson/traverson-hal/releases/new)
  - Tag version: `x.y.z` (without any prefix or suffix)
  - Target: The release branch that hast just been created
  - Release title === Tag version
  - empty description
  - add all four JS files from browser/dist as "binaries" to the release
  - Publish release
- Why not just create a tag from the branch via git? Because we want to add the build artifacts to the GitHub relase as attachments (for users not using npm). This is only possible if the release was created via GitHub's web interface. Normal git tags show up as releases there too, but you can't add attachments or edit the release afterwards. Releases created via the web interface create a git tag automatically, however.
- `git checkout master`
- `git branch -D release-x.y.z`
- `git push origin :release-x.y.z`
