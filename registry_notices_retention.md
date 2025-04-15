---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

keywords: IBM Cloud Container Registry notices, notices, retention policies

subcollection: Registry

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.registryshort}} introduces retention policies from 23 September 2019
{: #registry_notices_retention}

{{site.data.keyword.registrylong}} retention policies help keep your registry namespaces in check by retaining only the images that are important to you.
{: shortdesc}

The original announcement was published on 9 October 2019.
{: note}

{{site.data.keyword.registryshort}} now offers retention policies so that you can choose the number of images to retain in each repository in a namespace. You can use retention policies to decrease clutter, help meet storage quotas, and minimize storage costs.

When following continuous delivery practices, customers frequently push new images to their registry namespaces. Over time, the registry stores many images, though few might be needed or deployed anymore.

With retention policies, you can select a number of images to be retained for each repository in a specific namespace, and all other images in that namespace are deleted. The newest images are retained, with age determined by an image's creation date. You can run a retention policy once to do a quick cleanup, or it can be scheduled to run daily to continuously delete images that are outside your policy settings.

## Setting retention policies in the CLI
{: #registry_notices_retention_cli}

To set a retention policy, use the `ibmcloud cr retention-policy-set` command, which takes a number of images and a namespace as arguments. When you set a retention policy, the policy takes effect immediately, which means that images are deleted immediately to fulfill your policy, and the policy is also scheduled as a daily recurrence. The images that will be deleted are displayed, and a confirmation asks if you want to continue.

For example, the `retention-test` namespace has two repositories, `mysql` and `mongo`, each of which contains three images:

``` txt
$ ibmcloud cr images --restrict retention-test
Listing images...

Repository                      Tag     Digest        Namespace       Created      Size    Security status
uk.icr.io/retention-test/mongo  3.6.14  5d962dcc31f7  retention-test  2 weeks ago  165 MB  1 Issue
uk.icr.io/retention-test/mongo  4.0.12  b8bb45950dfb  retention-test  2 weeks ago  153 MB  1 Issue
uk.icr.io/retention-test/mongo  4.2     5de3b9233bae  retention-test  2 weeks ago  147 MB  1 Issue
uk.icr.io/retention-test/mysql  5.6     b8076d31e751  retention-test  3 weeks ago  83 MB   4 Issues
uk.icr.io/retention-test/mysql  5.6.43  5ab881bc5abe  retention-test  6 months ago 83 MB   4 Issues
uk.icr.io/retention-test/mysql  5.7.27  5c508e03f7f1  retention-test  3 weeks ago  124 MB  7 Issues

OK
```
{: screen}

In the example, two images are retained in each repository, which means that one image from each repository is deleted immediately.

```txt
$ ibmcloud cr retention-policy-set --images 2 retention-test
Image                                                       Tags
uk.icr.io/retention-test/mongo@sha256:5d962dcc31f7xxxxxxx   3.6.14
uk.icr.io/retention-test/mysql@sha256:5ab881bc5abexxxxxxx   5.6.43

Found 2 images to delete.

If you set this policy, the selected images are deleted immediately according to the rules that you set in your policy.
Deleted images are moved to your trash and can be restored for 30 days. Do you want to continue to set the policy? [y/N]> y
Deleting 2 images...

Successfully deleted 2 images.

OK
The scheduled retention policy to keep 2 images per repository in retention-test is set.

OK
```
{: screen}

You can list your retention policies by using the `ibmcloud cr retention-policy-list` command. The default policy is to retain all images, so every namespace in your account is displayed in this list.

```txt
$ ibmcloud cr retention-policy-list
Listing image retention policies for account 'AP Account' in registry 'uk.icr.io'...

Namespace       Images to retain
ap-test         All
retention-test  2

OK
```
{: screen}

Because scheduled retention policies automatically delete images to meet the policy's specifications, a trash is implemented to hold deleted images for 30 days after their deletion in case they need to be restored. Any deleted images, not just those images that are deleted by retention policies, initially move to the trash. You can view your trash by using the `ibmcloud cr trash-list` command:

```txt
$ ibmcloud cr trash-list --restrict retention-test
Listing the contents of the trash...

Digest                                                      Days until expiry  Tags
uk.icr.io/retention-test/mongo@sha256:5d962dcc31f7xxxxxxx   30                 3.6.14
uk.icr.io/retention-test/mysql@sha256:5ab881bc5abexxxxxxx   30                 5.6.43

OK
```
{: screen}

Images in the trash can't be pulled, but they can be restored to the registry with the `ibmcloud cr image-restore` command.

If you want to do a quick cleanup without setting a recurring policy, use the `ibmcloud cr retention-run` command in the same way.

Retention policies are only supported in the CLI.

## Learn more
{: #registry_notices_retention_learn}

Read more about retention policies in the documentation, see [Cleaning up your namespaces in {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_retention), and [update your `container-registry` CLI plug-in](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_cli_update) to give it a try.

## Original announcement
{: #registry_notices_retention_announce}

The original announcement was published on 9 October 2019.
