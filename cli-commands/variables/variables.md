# Azion CLI variables command and its subcommands

See the command and subcommands that enable the management of your environment variables on the Azion Edge Platform using **Azion CLI**.

> 1. [Listing your environment variables](#variables-list)
> 2. [Creating an environment variable](#variable-create)
> 3. [Updating an environment variable](#variable-update)
> 4. [Describing an environment variable](#variable-describe)
> 5. [Deleting an environment variable](#variable-delete)

---

## 1. Listing your environment variables {#variables-list}

List the environment variables set in your account.

### Usage

```bash
  azioncli variables list
```

### Optional flags

#### details

The `--details` option displays all relevant fields when listing.

#### help

The `--help` option displays more information about the `list` subcommand.

---

## 2. Creating an environment variable {#variable-create}

Create a new environment variable or secret to be used inside your edge functions.

### Usage

```bash
  azioncli variables create --key "Content-Type" --value "string" --secret false
```

### Required flags if the --in flag is not informed

#### key

The `--key` flag provides the variable's key.

#### value

The `--value` flag provides the variable's value.

#### secret

The `--secret` flag indicates whether the value is meant to be confidential. The default value is `true`.

### Optional flags

#### in

The `--in` flag informs the file path to the file containing all attributes of variable being created. You can use `-` for reading from stdin.

#### help

The `--help` option displays more information about the `create` subcommand.

---

## 3. Updating an environment variable {#variable-update}

Update an environment variable based on given attributes.

### Usage

```bash
  azioncli variables update --variable-id 7a187044-4a00-4a4a-93ed-d2309004019201909321f3 --key 'Content-Type' --value 'json' --secret false
```

### Required flags if the --in flag is not informed

#### variable-id

The `--variable-id` flag gives the UUID for the variable being updated.

#### key

The `--key` flag provides the variable's key.

#### value

The `--value` flag provides the variable's value.

#### secret

The `--secret` flag indicates whether the value is meant to be confidential. The default value is `true`.

### Optional flags

#### in

The `--in` flag informs the file path to the file containing all attributes of variable being updated. You can use `-` for reading from stdin.

#### help

The `--help` option displays more information about the `update` subcommand.

---

## 4. Describing an environment variable {#variable-describe}

Return details about a specific environment variable based on a given UUID.

### Usage

```bash
  azioncli variables describe --variable-id 1673635839
```

### Required flags

#### variable-id

The `--variable-id` flag gives the UUID for the variable being described.

### Optional flags

#### out

The `--out` option exports the output of the `describe` command to a given filepath.

#### format

The `--format` option, followed by the value `json`, changes the output format to JSON.

#### help

The `--help` option displays more information about the `describe` subcommand.

---

## 5. Deleting an environment variable {#variable-delete}

Delete an environment variable on the Azion platform.

### Usage

```bash
  azioncli variables delete --variable-id 7a187044-4a00-4a4a-93ed-d230900423221f3
```

### Required flags

#### variable-id

The `--variable-id` flag gives the UUID for the environment variable being deleted.

### Optional flags

#### help

The `--help` option displays more information about the `delete` subcommand.
