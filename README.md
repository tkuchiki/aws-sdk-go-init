# aws-sdk-go-config

---

```go
import "github.com/tkuchiki/aws-sdk-go-config"
```

## Usage

```go
const (
	// DefaultProfile is default profile name
	DefaultProfile = "default"
)
```

#### func  GetProfile

```go
func GetProfile() string
```
GetProfile returns the profile

#### func  GetProfiles

```go
func GetProfiles(configFile ...string) []string
```
GetProfiles returns the shared config file section names

#### func  GetRegion

```go
func GetRegion(profile string) string
```
GetRegion returns the region

#### func  GetRegionFromConfigFile

```go
func GetRegionFromConfigFile(configFile, profile string) (string, error)
```
GetRegionFromConfigFile returns the region from the shared config file

#### func  GetRegionFromInstanceIdentityDocument

```go
func GetRegionFromInstanceIdentityDocument() string
```
GetRegionFromInstanceIdentityDocument returns the region from the Instance
Metadata

#### func  GetSharedConfigFile

```go
func GetSharedConfigFile() string
```
GetSharedConfigFile returns the path to the shared config file

#### func  GetSharedCredentialsFile

```go
func GetSharedCredentialsFile() string
```
GetSharedCredentialsFile returns the path to the shared credentials file

#### func  NewConfig

```go
func NewConfig(opt Option) (*aws.Config, error)
```
NewConfig returns the *aws.Config

#### func  NewCredentials

```go
func NewCredentials(opt Option) (*credentials.Credentials, error)
```
NewCredentials returns the *credentials.Credentials

#### func  NewSession

```go
func NewSession(arg ...interface{}) (*session.Session, error)
```
NewSession returns the *session.Session.

The argument arg Option or *aws.Config

#### type Option

```go
type Option struct {
	// AWS Access Key ID
	AccessKey string
	// AWS Secret Access Key
	SecretKey string
	// AssumeRole Arn
	Arn string
	// AWS Profile
	Profile string
	// Path to the shared config file
	Config string
	// Path to the shared credentials file
	Credentials string
	// AWS Session Token
	Token string
	// AWS Region
	Region string
    // ExpiryWindow
    ExpiryWindow time.Duration
}
```

Option is AWS Config options

## Examples

```go
package main

import (
    "github.com/tkuchiki/aws-sdk-go-config"
    "github.com/aws/aws-sdk-go/aws"
    "github.com/aws/aws-sdk-go/aws/credentials"
    "github.com/aws/aws-sdk-go/aws/session"
    "log"
)

func main() {
    var creds *credentials.Credentials
    var err error
    creds, err = awsconfig.NewCredentials(awsconfig.Option{})
    if err != nil {
        log.Fatal(err)
    }

    var conf *aws.Config
    conf, err = awsconfig.NewConfig(awsconfig.Option{})
    if err != nil {
        log.Fatal(err)
    }

    var sess *session.Session
    sess, err = awsconfig.NewSession()
    //sess, err = awsconfig.NewSession(awsconfig.Option{})
    //sess, err = awsconfig.NewSession(conf)
    if err != nil {
        log.Fatal(err)
    }

    //fmt.Println(awsconfig.GetProfiles("/path/to/.aws/credentials"))
    //fmt.Println(awsconfig.GetProfiles())
}
```
