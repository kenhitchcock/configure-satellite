Role Name
=========

> This role was written to automate the configuration of satellite server from version 6.4 onwards.

Requirements
------------
 Satellite will need to be installed and registered to Red Hat network, the manifest will
 also need to be uploaded. Have a look at my satellite install role to assist with this.

 https://github.com/kenhitchcock/ansible-role-satellite-install

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

    # Platform you wish to deploy a Cornerstone VM onto
    rh_username:
    rh_password:

    # Requires that the activation key be precreated.
    rh_ak:

    # This can be found in your Red Hat online portal.
    # Or if using satellite this will be in the Organizations section.
    # First organization is normally 1
    rh_org:

    # Currently supports yes or no
    rh_forceregister:

    # Two dictionary lists are used by satellite-configure

    # First Dictionary should be removed in new versions
    configure_satellite_lifecycles:
      Production:
        organization: "MySpecialOrg"
        description: "Production life cycle"
        prior: "Library"

    # The Dict below should be used for all configurations. Each section is self explainatory. 
    # More customization to follow in future. 
    # Would also be nice if we could generate this content from somewhere based on customer requirements.
	configure_satellite_organizations:
	  - orgname: "MySpecialOrg"
	    contentviews:
	      - cv: "Cloudforms-CV"
	      - cv: "OpenShift3_11-CV"
	      - cv: "Openstack13-CV"
	      - cv: "RHEL7SOE-CV"
	      - cv: "RHVH-CV"
	    cvrepositories:
	      - cvrepo: "Red Hat CloudForms Management Engine 5.10 RPMs x86_64"
		product: "Red Hat CloudForms"
		cv: "Cloudforms-CV"
	      - cvrepo: "Red Hat Enterprise Linux 7 Server - Optional RPMs x86_64 7Server"
		product: "Red Hat Enterprise Linux Server"
		cv: "Cloudforms-CV"
	    sync_plans:
	      - syncplan: "Weekly Sync Plan"
		interval: "weekly"
		startdate: "2019-02-04 01:00:00"
		enabled: true
	    lifecycles:
	      - lc: ProdB
		description: "ProdB life cycle"
		prior: "Library"
	    activationkeys:
	      - ak: "Cloudforms-AK"
		lifecycle: ProdB
		contentview: Cloudforms-CV
	      - ak: "Openshift-AK"
		lifecycle: ProdB
		contentview: OpenShift3_11-CV
	      - ak: "Openstack-AK"
		lifecycle: ProdB
		contentview: Openstack13-CV
	      - ak: "RHEL7Server-AK"
		lifecycle: ProdB
		contentview: RHEL7SOE-CV
	    products:
	      - product: "Red Hat Enterprise Linux Server"
	      - product: "Red Hat Ansible Engine"
	      - product: "Red Hat OpenShift Container Platform"
	      - product: "Red Hat Software Collections (for RHEL Server)"
	      - product: "Red Hat Enterprise Linux High Availability for x86_64"
	    yum_repository:
	      - repo: "Red Hat Enterprise Linux 7 Server - Extras (RPMs)"
		basearch: "x86_64"
		releasever: "7Server"
		product: "Red Hat Enterprise Linux Server"
	      - repo: "Red Hat Enterprise Linux 7 Server (Kickstart)"
		basearch: "x86_64"
		releasever: "7Server"
		product: "Red Hat Enterprise Linux Server"
	    container_repository:
	      - repo: "Juniper Contrail"
		basearch: "x86_64"
		releasever: "7Server"
		product: "Juniper Contrail"
	      - repo: "OSP13 Containers"
		basearch: "x86_64"
		releasever: "7Server"


Future Releases
---------------

 - Add support for more automation.
 - make use of new hammer modules once the appear.

License
-------

MIT

Author Information
------------------

Ken Hitchcock [Github](https://github.com/kenhitchcock)

