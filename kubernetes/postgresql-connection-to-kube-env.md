# Postgresql connection to Kube env

```text
kubectl run -it --rm psql --image=postgres /bin/bash
psql -h <host> -U <user> -d <db_name>

# After done
kubectl delete pod psql
```

