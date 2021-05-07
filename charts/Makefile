TOPDIR=..
REALTOP=$(shell readlink -f ..)
#include $(TOPDIR)/Makefiles/Repo-defines.mk

OPERATOR_CHART_DIR=redis-cluster-operator
REDIS_CLUSTER_CHART_DIR=empirix-redis-cluster


J2=j2
HELM=helm

# ------------------------------------------------------------------------------------------
# GNU make targets
# ------------------------------------------------------------------------------------------

.PHONY: packaging clean

clean:
#	$(RM) -f $(CHART_DIR)/values.yaml
#	$(RM) -f $(CHART_DIR)/Chart.yaml
#	$(RM) -f $(CHART_DIR)-$(DOCKER_VERSION).tgz
	$(RM) -f $(REDIS_CLUSTER_CHART_DIR)/charts/*
	$(RM) -f $(REDIS_CLUSTER_CHART_DIR)/Chart.lock

packaging: clean
	# embed some values known to the build system (GNU make) into the final values.yaml
#	CHART_NAME=$(CHART_DIR) \
#	REMOTE_REPO_NEXUS_DOCKER_FOR_PULL=$(REMOTE_REPO_NEXUS_DOCKER_FOR_PULL)/ \
#	DOCKER_GROUP=$(DOCKER_GROUP)/ \
#		$(J2) $(CHART_DIR)/values.yaml.j2 -o $(CHART_DIR)/values.yaml

	# embed some values known to the build system (GNU make) into the final Chart.yaml
#	CHART_NAME=$(CHART_DIR) \
#	HELM_VERSION=$(HELM_VERSION) \
#	DOCKER_VERSION=$(DOCKER_VERSION) \
#		$(J2) $(CHART_DIR)/Chart.yaml.j2 -o $(CHART_DIR)/Chart.yaml

	# run Helm lint
	$(HELM) lint $(OPERATOR_CHART_DIR)

	# run Helm package
	$(HELM) package $(OPERATOR_CHART_DIR)

	# run Helm dependency build
	$(HELM) dependency build $(REDIS_CLUSTER_CHART_DIR)

	# run Helm lint
	$(HELM) lint $(REDIS_CLUSTER_CHART_DIR)

	# run Helm package
	$(HELM) package $(REDIS_CLUSTER_CHART_DIR)

