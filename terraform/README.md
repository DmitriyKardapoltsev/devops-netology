# Local .terraform directories
Повторное описание, предыдущая версия не сохранилась
Указаны файлы для исключения
**/.terraform/* - в любой директории репозитория в данном файле

# Исключает все файлы данного типа.tfstate files
*.tfstate
*.tfstate.*

# Crash log files
crash.log - исключает такие файлы
crash.*.log

# Exclude all .tfvars files, which are likely to contain sensitive data, such as
# password, private keys, and other secrets. These should not be part of version 
# control as they are data points which are potentially sensitive and subject 
# to change depending on the environment.
*.tfvars - исключает файлы данного типа
*.tfvars.json

# Ignore override files as they are usually used to override resources locally and so
# are not checked in
override.tf
override.tf.json
*_override.tf
*_override.tf.json

# Include override files you do wish to add to version control using negated pattern
# !example_override.tf - файл с таким имененем попадает под исключение из правила по игнорированию

# Include tfplan files to ignore the plan output of command: terraform plan -out=tfplan
# example: *tfplan*

# Ignore CLI configuration files
.terraformrc
terraform.rc