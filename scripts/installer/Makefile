INSTALLER_ZIP_DIR=dvinstall
DATAVERSE_WAR_FILE=${INSTALLER_ZIP_DIR}/dataverse-4.0.war
GLASSFISH_SETUP_SCRIPT=${INSTALLER_ZIP_DIR}/glassfish-setup.sh
POSTGRES_DRIVERS=${INSTALLER_ZIP_DIR}/pgdriver
API_SCRIPTS=${INSTALLER_ZIP_DIR}/setup-datasetfields.sh ${INSTALLER_ZIP_DIR}/setup-users.sh ${INSTALLER_ZIP_DIR}/setup-builtin-roles.sh ${INSTALLER_ZIP_DIR}/setup-dvs.sh ${INSTALLER_ZIP_DIR}/data ${INSTALLER_ZIP_DIR}/setup-identity-providers.sh  ${INSTALLER_ZIP_DIR}/setup-all.sh 
DB_SCRIPT=${INSTALLER_ZIP_DIR}/reference_data.sql
JHOVE_CONFIG=${INSTALLER_ZIP_DIR}/jhove.conf
SOLR_SCHEMA=${INSTALLER_ZIP_DIR}/schema.xml
INSTALL_SCRIPT=${INSTALLER_ZIP_DIR}/install

installer:	dvinstall.zip

dvinstall.zip:	${GLASSFISH_SETUP_SCRIPT} ${POSTGRES_DRIVERS} ${DATAVERSE_WAR_FILE} ${API_SCRIPTS} ${DB_SCRIPT} ${JHOVE_CONFIG} ${INSTALL_SCRIPT}
	@echo making installer...
	zip -r dvinstall.zip ${GLASSFISH_SETUP_SCRIPT} ${POSTGRES_DRIVERS} ${DATAVERSE_WAR_FILE} ${API_SCRIPTS} ${DB_SCRIPT} ${JHOVE_CONFIG} ${SOLR_SCHEMA} ${INSTALL_SCRIPT}
	@echo 
	@echo "Done!"

${INSTALL_SCRIPT}: install
	echo copying the installer script
	mkdir -p ${INSTALLER_ZIP_DIR}
	/bin/cp install ${INSTALLER_ZIP_DIR}



${DATAVERSE_WAR_FILE}:	../../target/dataverse-4.0.war
	@echo copying war file...
	@mkdir -p ${INSTALLER_ZIP_DIR}
	/bin/cp ../../target/dataverse-4.0.war ${DATAVERSE_WAR_FILE}

../../target/dataverse-4.0.war:
	@echo
	@echo "ERROR: can't find application .war file (../../target/dataverse-4.0.war)!"
	@echo "Build the DVN war file, then try again."
	@echo
	@exit 1

${GLASSFISH_SETUP_SCRIPT}:	glassfish-setup.sh
	echo copying glassfish setup
	mkdir -p ${INSTALLER_ZIP_DIR}
	/bin/cp glassfish-setup.sh ${INSTALLER_ZIP_DIR}


${POSTGRES_DRIVERS}:	pgdriver/postgresql-8.4-703.jdbc4.jar pgdriver/postgresql-9.0-802.jdbc4.jar pgdriver/postgresql-9.1-902.jdbc4.jar
	echo copying postgres drviers
	@mkdir -p ${POSTGRES_DRIVERS}
	/bin/cp pgdriver/postgresql-8.4-703.jdbc4.jar pgdriver/postgresql-9.0-802.jdbc4.jar pgdriver/postgresql-9.1-902.jdbc4.jar ${INSTALLER_ZIP_DIR}/pgdriver

${API_SCRIPTS}:	../api/setup-datasetfields.sh ../api/setup-users.sh ../api/setup-dvs.sh ../api/setup-identity-providers.sh ../api/setup-all.sh ../api/setup-builtin-roles.sh ../api/data ../api/data
	echo copying api scripts
	@mkdir -p ${INSTALLER_ZIP_DIR}
	/bin/cp -R ../api/setup-datasetfields.sh ../api/setup-users.sh ../api/setup-dvs.sh ../api/setup-identity-providers.sh ../api/setup-all.sh ../api/setup-builtin-roles.sh ../api/data ${INSTALLER_ZIP_DIR}

${DB_SCRIPT}:	../database/reference_data.sql
	echo copying reference data sql script
	@mkdir -p ${INSTALLER_ZIP_DIR}
	/bin/cp ../database/reference_data.sql ${INSTALLER_ZIP_DIR}

${JHOVE_CONFIG}:	../../conf/jhove/jhove.conf
	echo copying jhove config file
	@mkdir -p ${INSTALLER_ZIP_DIR}
	/bin/cp ../../conf/jhove/jhove.conf ${INSTALLER_ZIP_DIR}

${SOLR_SCHEMA}:	../../conf/solr/4.6.0/schema.xml
	echo copying Solr schema file
	@mkdir -p ${INSTALLER_ZIP_DIR}
	/bin/cp ../../conf/solr/4.6.0/schema.xml ${INSTALLER_ZIP_DIR}
