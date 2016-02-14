# Introduction #

The module hooks into the AuthenticationService by using AOP and enforces a number of policy constraints to prevent the creation of unsecure passwords and to prevent a password from beeing used multiple times.


# Installation #

  * Download the sources and provide the alfresco specific dependencies in your local maven repo.
  * Create your IDE specific project by using `mvn eclipse:eclipse`.
  * Build the project by using `mvn install`. The build process contains a default profile that copies the packaged artifact to a pre defined Alfresco installation.

# Architecture and Design #
The module intercepts all attempts to change a users password using a Spring AOP interceptor and delegates it to a AuthenticationServiceAdvice. The new password is verified against a number of configurable constraints.

## Password Constraints ##
All constraints are configured within the custom-authentication-context.xml bean config.

### Password Similarity Constraint ###
The "Password Similarity Constraint" ensures that the old and the new password are not equal.

```
    <bean id="passwordSimilarityConstraint" class="org.alfresco.extension.authentication.constraint.PasswordSimilarityConstraint">
        <property name="allowEqualPasswords" value="false" />
    </bean>
```

### Password History Constraint ###
The "Password History Constraint" compares the new password with previous passwords. As Alfresco does not store a password history by default, the constraint takes care of it.
When a user tries to change his password, the constraint checks if a password history aspect is present on the user's cm:person object and adds it if the aspect is not present.
All new passwords are encrypted with an SHA-1 encoder and added to the history. The history keeps the defined number of password hashes and removes the first history entry if the defined maximum number of passwords is exceeded.
The new password's has value is compared to the existing hashes from the history aspect.

```
    <bean id="passwordHistoryConstraint" class="org.alfresco.extension.authentication.constraint.PasswordHistoryConstraint" >
        <property name="nodeService" ref="nodeService" />
        <property name="personService" ref="personService" />
        <!-- Set to -1 to disable the history-->
        <property name="maxHistoryEntries" value="3" />
    </bean>
```


### Password Regex Constraint ###
The "Password Regex Constraint" matches the new password to a number of regular expression patterns. By constraint asserts that the password contains at least 1 special character and 1 upper case letter.

```

    <bean id="passwordRegexConstraint" class="org.alfresco.extension.authentication.constraint.PasswordRegexConstraint">
        <property name="allowPatterns"  >
            <list>
                <value>^.*(?=.*[\d\W]).*$</value>
                <value>^.*(?=.*[A-Z]).*$</value>
            </list>
        </property>
    </bean>
    
```