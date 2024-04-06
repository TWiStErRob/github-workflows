# Release Process

1. [Draft a new release on GitHub](https://github.com/TWiStErRob/github-workflows/releases/new).
2. Generate release notes
3. Review changes to determine the next version number.
4. Change tag and name to the next version number. (vX.Y.Z)
5. If it's a major release, update README.md `@vX` references with a "Prepare vX" PR.
6. Publish the release.
7. Locally finalize the moving tag:
   ```shell
   git fetch
   git checkout vX.Y.Z
   git tag vX
   git push origin vX -f
   ```

# Versioning
Trying to follow semver.

Interface changes are usually breaking, for example adding a permission to a job.
