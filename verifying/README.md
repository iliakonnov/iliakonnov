# TSA
From time to time I add trusted timestamps to my Git commits.

See [this SO question](https://stackoverflow.com/q/11913228) for more details.

You can find and check such commits in any repo using following command:
```bash
# Get certificate from freeTSA.org
wget https://freetsa.org/files/cacert.pem -O freetsa-cacert.pem
echo "2151b61137ffa86bf664691ba67e7da0b19f98c758e3d228d5d8ebf27e044438  freetsa-cacert.pem" | sha256sum -c

# You should fetch notes first
git fetch origin "refs/notes/*:refs/notes/*"
git rev-list master | ./git-timestamp -l verify - | grep -v 'No trusted timestamp'
```

# GPG
You can also verify commits using GPG.
```bash
echo "54c1b120a2a5112a62c72a6b3d2947675372ce534d84ee9028f7be11b3ac276d  gpg.pub" | sha256sum -c
gpg --import < gpg.pub
git log --pretty=format:'%h %C(auto,green)G%C(reset) %ad %an'
```
