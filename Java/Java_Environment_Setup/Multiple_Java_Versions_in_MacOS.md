# Multiple Java Versions in MacOS
> Mac에서 여러개의 Java version을 관리하기
> 
> References: [jenv.be](https://www.jenv.be/), [how-to-manage-multiple-java-version-in-macos](https://chamikakasun.medium.com/how-to-manage-multiple-java-version-in-macos-e5421345f6d0)

<br>
<br>

Install Java version manager - `jenv`

```bash
brew install jenv
```

<br>

Add followings to shell config file - `~/.zshrc`

```bash
export PATH="$HOME/.jenv/bin:$PATH"
eval "$(jenv init -)"
```

And then run `source ~/.zshrc` of course

<br>

Run following commands (if you are using maven)

```bash
# ensure that JAVA_HOME is correct
jenv enable-plugin export
# make Maven aware of the Java version in use (and switch when your project does)
jenv enable-plugin maven
```
<br>

Install different JDK versions

```bash
brew install java

# For older Java versions, use this command
brew install AdoptOpenJDK/openjdk/adoptopenjdk{11,14}

# or you can install a single version as follows:
brew install AdoptOpenJDK/openjdk/adoptopenjdk8
```
<br>

See all the installed JDK versions in your machine

```bash
/usr/libexec/java_home -V
```

<br>

Add to `jEnv` each of the JDK you installed by the following command

```bash
jenv add <your_jdk_path>

# Example:
jenv add /Library/Java/JavaVirtualMachines/openjdk-14.0.1.jdk/Contents/Home
```

<br>

See whether all the versions you add are available in the `jEnv`

```bash
jenv versions
```

<br>

Setting system-wide Java version

```bash
jenv global 11
```

<br>

Setting project-wide Java version

```bash
jenv local 8
```

<br>

Setting shell instance Java version

```bash
jenv shell openjdk64-1.8.0.252
```
<br>

Checking current Java version

```bash
java -version
```
