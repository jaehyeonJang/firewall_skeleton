# @@@LICENSE
#
# Copyright (c) 2022 LG Electronics, Inc.
#
# Confidential computer software. Valid license from LG required for
# possession, use or copying. Consistent with FAR 12.211 and 12.212,
# Commercial Computer Software, Computer Software Documentation, and
# Technical Data for Commercial Items are licensed to the U.S. Government
# under vendor's standard commercial license.
#
# LICENSE@@@

cmake_minimum_required (VERSION 2.8.7)
project (network-firewall)
find_package(PkgConfig REQUIRED)

# Check xtables
pkg_check_modules(XTABLES REQUIRED xtables)

# Configuration File
install (FILES firewall_archive/init/firewall-manager
        DESTINATION ${CMAKE_INSTALL_PREFIX}/bin/
        PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
        COMPONENT configurations
)

set(SERVICE_FILE "firewall_archive/init/firewall-manager.service")
install (FILES ${SERVICE_FILE}
        DESTINATION ${CMAKE_INSTALL_PREFIX}/lib/systemd/system/
	PERMISSIONS OWNER_WRITE OWNER_READ GROUP_READ WORLD_READ
	COMPONENT configurations
)

set(POLICIES  "firewall_archive/rule/*.conf")
install (FILES ${POLICIES}
        DESTINATION ${CMAKE_INSTALL_PREFIX}/etc/firewall-manager/
        PERMISSIONS OWNER_WRITE OWNER_READ
        COMPONENT configurations
)
