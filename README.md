# kubernetesDocs
<br/> https://kubernetes.io <br/>

<p>Kubernetes fonctionne sur la base d'un état défini et d'un état réel. Les objets Kubernetes représentent l'état d'un cluster. Ils indiquent à Kubernetes à quoi vous voulez que la charge de travail ressemble. Une fois qu'un objet a été créé et défini, Kubernetes veille à ce qu'il soit toujours présent.</p>
<h2>BASH</h2>
> source <(kubectl completion bash) # setup autocomplete in bash into the current shell, bash-completion package should be installed first. <br/>
> echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell. <br/>
<h2>Kubectl context and configuration</h2>

<code>

kubectl config view # Show Merged kubeconfig settings.

# use multiple kubeconfig files at the same time and view merged config
KUBECONFIG=~/.kube/config:~/.kube/kubconfig2

kubectl config view

# get the password for the e2e user
kubectl config view -o jsonpath='{.users[?(@.name == "e2e")].user.password}'

kubectl config view -o jsonpath='{.users[].name}'    # display the first user
kubectl config view -o jsonpath='{.users[*].name}'   # get a list of users
kubectl config get-contexts                          # display list of contexts
kubectl config current-context                       # display the current-context
kubectl config use-context my-cluster-name           # set the default context to my-cluster-name

# add a new user to your kubeconf that supports basic auth
kubectl config set-credentials kubeuser/foo.kubernetes.com --username=kubeuser --password=kubepassword

# permanently save the namespace for all subsequent kubectl commands in that context.
kubectl config set-context --current --namespace=ggckad-s2

# set a context utilizing a specific username and namespace.
kubectl config set-context gce --user=cluster-admin --namespace=foo \
  && kubectl config use-context gce

kubectl config unset users.foo                       # delete user foo

# short alias to set/show context/namespace (only works for bash and bash-compatible shells, current context to be set before using kn to set namespace) 
alias kx='f() { [ "$1" ] && kubectl config use-context $1 || kubectl config current-context ; } ; f'
alias kn='f() { [ "$1" ] && kubectl config set-context --current --namespace $1 || kubectl config view --minify | grep namespace | cut -d" " -f6 ; } ; f'
  
</code>
