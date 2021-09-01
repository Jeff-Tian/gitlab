gitlab-ee with Keycloak login enabled

---

## Screenshot

## Set up

```shell
docker-compose up -d
# SSH into the GitLab server and take the backup of gitlab.rb file.
cd /etc/gitlab
# Now open the gitlab.rb in vim or nano and paste the following lines at the start/end of the file & save it.
vi gitlab.rb
gitlab-ctl reconfigure
open https://gitlab.example.com/8929
# login with root/secret_pass for admin
# login with Keycloak for user  
```

## Pasting text

```ruby
gitlab_rails['omniauth_enabled'] = true
gitlab_rails['omniauth_allow_single_sign_on'] = ['saml']
# gitlab_rails['omniauth_auto_sign_in_with_provider'] = 'saml'
gitlab_rails['omniauth_block_auto_created_users'] = false
# gitlab_rails['omniauth_auto_link_ldap_user'] = false
gitlab_rails['omniauth_auto_link_saml_user'] = true
gitlab_rails['omniauth_providers'] = [
    {
        name: 'saml',
        args: {
            assertion_consumer_service_url: 'https://jeff-tian-gitlab-wq766wrh9r57-8929.githubpreview.dev/users/auth/saml/callback',
            idp_cert: " -----BEGIN CERTIFICATE-----
\n MIICnzCCAYcCBgFyRsZ81zANBgkqhkiG9w0BAQsFADATMREwDwYDVQQDDAhVbmlIZWFydDAeFw0yMDA1MjQxMzAwMTJaFw0zMDA1MjQxMzAxNTJaMBMxETAPBgNVBAMMCFVuaUhlYXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoHEhTT5e1gg5N4zchLALb3bmVyapIBhUP031h7Hbj6BTSdZRNIdm7fMXVNvxQJMPrOLAFKpt4eNRsE0evD+KoByYiZFq5FNMLOUcTGBH2idijehTAwbl3auhUKHswXGi7M76HdiP2P8NsS9oMHEZwmW4uRuu1egHjNAoH//alHQN39MjytmBBVXHJsAXqfP2i/1UfBOb5UaJ6szvY1OsAzUXrd0q1g61xNQJkjUNmT3FLWfh+VKaNdxcRvMxybg6Sq+POMxsIx/Ojy9cYa2PsC0eZyJdpWSnbpDKu2wa2T2KLzAhyqev+3+8u81fcfjeRRguhRJZXpyvGlRuaHbIZwIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQAhy49rW9hGNyDeJnkPEdHy5SCSWf4JX8oSA3OxAqokOjfV6NWQ2sDpFZWWIqX3kQmSDwgOs3vlQBgWTopzuVDVy6IsWZ/WWjLguHpEVh781QLwqqvayaUWtyP6BA0bCPkHhFBopnJgf9iX5evJ4aZMcwNT5aF41SOf0zvhc4Vo3pOOls1rLfX1SBbRXuy1Nc5fpTZ02Ip9Z3v8nezmSwp9s9378+8kWW1C8+nFoY5mxU8uFE533Og9zN+uL/BokAxlhP5wcM63gksnvKnGf4cUuHq0nvi5jTbziena7ZO9L+BmPy1uJJtQ16LaMSd3/gVl9kxM8CQosmWWDcIuuyzU\n -----END CERTIFICATE----- \n",
            idp_sso_target_url: 'https://keycloak.jiwai.win/auth/realms/UniHeart/protocol/saml/clients/jeff-tian-gitlab-wq766wrh9r57-8929.githubpreview.dev',
            issuer: 'jeff-tian-gitlab-wq766wrh9r57-8929.githubpreview.dev',
            name_identifier_format: 'urn:oasis:names:tc:SAML:2.0:nameid-format:persistent'
        },
        label: 'KEYCLOAK 登录'
    }
]
```
