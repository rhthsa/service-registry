# Create Realm for Service Registry

1. Switch to **Administrator** view then click **Installed Operators** and **Red Hat Single Sign-On Operator**, and click the Keycloak Realm tab, and then **Create KeycloakRealm** button to create a new realm.

   ![Realm setup](../../images/sso-realm-setup-1.png)

   ![Realm setup](../../images/sso-realm-setup-2.png)

2. Change to **YAML view** then copy the conent in [keycloak-realm.yaml](../../manifest/keycloak-realm.yaml) and past into the editor. Edit the realm name, redirectUris, webOrigins, username, password etc. values as you need. Then click on **Create** button.

   > You must customize this KeycloakRealm resource with values suitable for your environment if you are deploying to production i.e. **realm name, redirectUris, webOrigins, username, password** etc. You can also create and manage realms using the Red Hat Single Sign-On web console.

   The configuration in [keycloak-realm.yaml](../../manifest/keycloak-realm.yaml) file will create following resources in SSO/Keycloak:

   **Realm**

   | **ID**       | **Display Name** |
   |----------|--------------|
   | registry | Registry     |

   **Role**

   | **Name**     | **Capabilities**                                                                                                                    |
   |--------------|-------------------------------------------------------------------------------------------------------------------------------------|
   | sr-admin     | Full access, no restrictions.                                                                                                       |
   | sr-developer | Create artifacts and configure artifact rules. Cannot modify global rules, perform import/export, or use `/admin`  REST API endpoint. |
   | sr-readonly  | View and search only. Cannot modify artifacts or rules, perform import/export, or use   `/admin`  REST API endpoint.                  |

   **Client**

   | **Client ID**           | **Description**                                           |
   |---------------------|-------------------------------------------------------|
   | registry-client-ui  | Keycloak client used by Service Registry web console. |
   | registry-client-api | Used by Service Registry API client.                  |

   **User**

   | **Username**       | **Password** | **Role**     |
   |--------------------|--------------|--------------|
   | registry-admin     | changeme     | sr-admin     |
   | registry-developer | changeme     | sr-developer |
   | registry-user      | changeme     | sr-readonly  |

   ![Realm setup](../../images/sso-realm-setup-3.png)

3. Go to **Workloads -> Secrets** menu, look for `credential-keycloak` secret and click on it. Then click on **Reveal values** link to see Keycloak Admin username and password.

   ![Realm setup](../../images/sso-realm-setup-4.png)

   ![Realm setup](../../images/sso-realm-setup-5.png)

4. Open Keycloak web console, click on **Administration Console** link. Then sign in with username and password from the previous step.

   ![Realm setup](../../images/sso-operator-installation-11.png)

   ![Realm setup](../../images/sso-realm-setup-6.png)

5. Select the **Registry** realm (or the realm you've just created above), then click **Users** menu, and then click **View all users** button. You should be able to see a list of users as configured in YAML in the **step 2** above.

   ![Realm setup](../../images/sso-realm-setup-7.png)
