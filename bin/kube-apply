
if [ -z "$YAML_PATH" ] && [ -z "$YAML_CONTENT" ]
then
	echo "Path or content must be specified!"
	exit 1
fi

if [ -n "$YAML_CONTENT" ]
then
YAML_PATH="./.cicd_apply.yaml"
cat <<EOF> $YAML_PATH
$YAML_CONTENT
EOF
fi

if [ ! -f "$YAML_PATH" ]
then
	echo "File \"$YAML_PATH\" not found! "
	exit 1
fi

if [ -z "$CICD_REGISTRY" ]
then
	CICD_REGISTRY=$CICD_LOCAL_REGISTRY
fi

if [ -n "$CICD_IMAGE_REPO" ]
then
	CICD_IMAGE="$CICD_REGISTRY/$CICD_IMAGE_REPO"
fi

echo "perform env var substitution"
sed -i 's^${CICD_LOCAL_REGISTRY}^'"$CICD_LOCAL_REGISTRY^g" "$YAML_PATH"
sed -i 's^${CICD_GIT_COMMIT}^'"$CICD_GIT_COMMIT^g" "$YAML_PATH"
sed -i 's^${CICD_GIT_REPO_NAME}^'"$CICD_GIT_REPO_NAME^g" "$YAML_PATH"
sed -i 's^${CICD_GIT_BRANCH}^'"$CICD_GIT_BRANCH^g" "$YAML_PATH"
sed -i 's^${CICD_GIT_REF}^'"$CICD_GIT_REF^g" "$YAML_PATH"
sed -i 's^${CICD_GIT_URL}^'"$CICD_GIT_URL^g" "$YAML_PATH"
sed -i 's^${CICD_GIT_TAG}^'"$CICD_GIT_TAG^g" "$YAML_PATH"
sed -i 's^${CICD_PIPELINE_ID}^'"$CICD_PIPELINE_ID^g" "$YAML_PATH"
sed -i 's^${CICD_TRIGGER_TYPE}^'"$CICD_TRIGGER_TYPE^g" "$YAML_PATH"
sed -i 's^${CICD_EXECUTION_ID}^'"$CICD_EXECUTION_ID^g" "$YAML_PATH"
sed -i 's^${CICD_EXECUTION_SEQUENCE}^'"$CICD_EXECUTION_SEQUENCE^g" "$YAML_PATH"
sed -i 's^${CICD_EVENT}^'"$CICD_EVENT^g" "$YAML_PATH"
sed -i 's^${CICD_CLUSTER_ID}^'"$CICD_CLUSTER_ID^g" "$YAML_PATH"
sed -i 's^${CICD_PROJECT_ID}^'"$CICD_PROJECT_ID^g" "$YAML_PATH"
sed -i 's^${CICD_REGISTRY}^'"$CICD_REGISTRY^g" "$YAML_PATH"
sed -i 's^${CICD_IMAGE}^'"$CICD_IMAGE^g" "$YAML_PATH"

kubectl apply -f "$YAML_PATH"
