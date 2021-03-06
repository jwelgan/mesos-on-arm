# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# COMPILE PROTOBUF STRUCTS REQUIRED TO BUILD MESOS.
###################################################
include(MesosProtobuf)

# Build the protobuf structs.
PROTOC_TO_INCLUDE_DIR(MESOS            mesos/mesos)
PROTOC_TO_INCLUDE_DIR(V1_MESOS         mesos/v1/mesos)
PROTOC_TO_INCLUDE_DIR(AUTHENTICATION   mesos/authentication/authentication)
PROTOC_TO_INCLUDE_DIR(AUTHORIZATION    mesos/authorizer/authorizer)
PROTOC_TO_INCLUDE_DIR(CONTAINERIZER    mesos/containerizer/containerizer)
PROTOC_TO_INCLUDE_DIR(EXECUTOR         mesos/executor/executor)
PROTOC_TO_INCLUDE_DIR(V1_EXECUTOR      mesos/v1/executor/executor)
PROTOC_TO_INCLUDE_DIR(FETCHER          mesos/fetcher/fetcher)
PROTOC_TO_INCLUDE_DIR(MAINTENANCE      mesos/maintenance/maintenance)
PROTOC_TO_INCLUDE_DIR(ALLOCATOR        mesos/master/allocator)
PROTOC_TO_INCLUDE_DIR(QUOTA            mesos/master/quota)
PROTOC_TO_INCLUDE_DIR(MODULE           mesos/module/module)
PROTOC_TO_INCLUDE_DIR(SCHEDULER        mesos/scheduler/scheduler)
PROTOC_TO_INCLUDE_DIR(V1_SCHEDULER     mesos/v1/scheduler/scheduler)
PROTOC_TO_INCLUDE_DIR(ISOLATOR         mesos/slave/isolator)
PROTOC_TO_INCLUDE_DIR(OVERSUBSCRIPTION mesos/slave/oversubscription)

PROTOC_TO_SRC_DIR(MESSAGES messages/messages)
PROTOC_TO_SRC_DIR(FLAGS    messages/flags)
PROTOC_TO_SRC_DIR(STATE    messages/state)
PROTOC_TO_SRC_DIR(REGISTRY master/registry)

set(MESOS_PROTOBUF_SRC
  ${MESOS_PROTO_CC}
  ${V1_MESOS_PROTO_CC}
  ${AUTHENTICATION_PROTO_CC}
  ${AUTHORIZATION_PROTO_CC}
  ${CONTAINERIZER_PROTO_CC}
  ${EXECUTOR_PROTO_CC}
  ${V1_EXECUTOR_PROTO_CC}
  ${FETCHER_PROTO_CC}
  ${MAINTENANCE_PROTO_CC}
  ${ALLOCATOR_PROTO_CC}
  ${QUOTA_PROTO_CC}
  ${MODULE_PROTO_CC}
  ${SCHEDULER_PROTO_CC}
  ${V1_SCHEDULER_PROTO_CC}
  ${OVERSUBSCRIPTION_PROTO_CC}
  ${MESSAGES_PROTO_CC}
  ${FLAGS_PROTO_CC}
  ${STATE_PROTO_CC}
  ${ISOLATOR_PROTO_CC}
  ${REGISTRY_PROTO_CC}
  )

# Configure Mesos files.
########################
configure_file(
  ${MESOS_PUBLIC_INCLUDE_DIR}/mesos/version.hpp.in
  ${MESOS_BIN_INCLUDE_DIR}/mesos/version.hpp
  )

# SOURCE FILES FOR THE MESOS LIBRARY.
#####################################
set(AUTHENTICATION_SRC
  authentication/cram_md5/authenticatee.cpp
  authentication/cram_md5/authenticator.cpp
  authentication/cram_md5/auxprop.cpp
  )

set(AUTHORIZER_SRC
  authorizer/authorizer.cpp
  authorizer/local/authorizer.cpp
  )

set(COMMON_SRC
  common/attributes.cpp
  common/date_utils.cpp
  common/http.cpp
  common/protobuf_utils.cpp
  common/resources.cpp
  common/resources_utils.cpp
  common/type_utils.cpp
  common/values.cpp
  )

set(DOCKER_SRC
  docker/docker.hpp
  docker/docker.cpp
  docker/executor.hpp
  )

set(EXEC_SRC
  exec/exec.cpp
  )

set(FILES_SRC
  files/files.cpp
  )

set(HOOK_SRC
  hook/manager.cpp
  )

set(INTERNAL_SRC
  internal/devolve.cpp
  internal/evolve.cpp
  )

set(LOCAL_SRC
  local/local.cpp
  )

set(LOGGING_SRC
  logging/flags.cpp
  logging/logging.cpp
  )

set(MASTER_SRC
  master/contender.cpp
  master/constants.cpp
  master/detector.cpp
  master/flags.cpp
  master/http.cpp
  master/maintenance.cpp
  master/master.cpp
  master/metrics.cpp
  master/registry.hpp
  master/registry.proto
  master/registrar.cpp
  master/repairer.cpp
  master/validation.cpp
  master/allocator/allocator.cpp
  master/allocator/sorter/drf/sorter.cpp
  )

set(MODULE_SRC
  module/manager.cpp
  )

set(SCHED_SRC
  sched/constants.cpp
  sched/sched.cpp
  )

set(SCHEDULER_SRC
  scheduler/scheduler.cpp
  )

set(AGENT_SRC
  slave/constants.cpp
  slave/gc.cpp
  slave/flags.cpp
  slave/http.cpp
  slave/metrics.cpp
  slave/monitor.cpp
  slave/paths.cpp
  slave/qos_controller.cpp
  slave/qos_controllers/noop.cpp
  slave/resource_estimator.cpp
  slave/slave.cpp
  slave/state.cpp
  slave/status_update_manager.cpp
  slave/containerizer/containerizer.cpp
  slave/containerizer/composing.cpp
  slave/containerizer/composing.hpp
  slave/containerizer/docker.cpp
  slave/containerizer/docker.hpp
  slave/containerizer/external_containerizer.cpp
  slave/containerizer/fetcher.cpp
  slave/containerizer/isolator.cpp
  slave/containerizer/isolators/filesystem/posix.cpp
  slave/containerizer/isolators/posix/disk.cpp
  slave/containerizer/launcher.cpp
  slave/containerizer/mesos/containerizer.cpp
  slave/containerizer/mesos/launch.cpp
  slave/containerizer/provisioner/paths.cpp
  slave/containerizer/provisioner/provisioner.cpp
  slave/containerizer/provisioner/store.cpp
  slave/containerizer/provisioner/appc/paths.cpp
  slave/containerizer/provisioner/appc/spec.cpp
  slave/containerizer/provisioner/appc/store.cpp
  slave/containerizer/provisioner/backend.cpp
  slave/containerizer/provisioner/backends/copy.cpp
  slave/containerizer/provisioner/docker/registry_client.cpp
  slave/containerizer/provisioner/docker/token_manager.cpp
  slave/resource_estimators/noop.cpp
  )

set(USAGE_SRC
  usage/usage.cpp
  )

set(V1_SRC
  v1/attributes.cpp
  v1/mesos.cpp
  v1/resources.cpp
  v1/values.cpp
  )

set(WATCHER_SRC
  watcher/whitelist_watcher.cpp
  )

set(ZOOKEEPER_SRC
  zookeeper/contender.cpp
  zookeeper/detector.cpp
  zookeeper/zookeeper.cpp
  zookeeper/authentication.cpp
  zookeeper/group.cpp
  )

set(MESOS_SRC
  ${MESOS_SRC}
  ${AUTHENTICATION_SRC}
  ${AUTHORIZER_SRC}
  ${COMMON_SRC}
  ${DOCKER_SRC}
  ${EXEC_SRC}
  ${FILES_SRC}
  ${HOOK_SRC}
  ${INTERNAL_SRC}
  ${LOCAL_SRC}
  ${LOGGING_SRC}
  ${MASTER_SRC}
  ${MODULE_SRC}
  ${SCHED_SRC}
  ${SCHEDULER_SRC}
  ${AGENT_SRC}
  ${USAGE_SRC}
  ${V1_SRC}
  ${WATCHER_SRC}
  ${ZOOKEEPER_SRC}
  ${MESOS_PROTOBUF_SRC}
  )

# INCLUDE DIRECTIVES FOR MESOS LIBRARY (generates, e.g., -I/path/to/thing
# on Linux).
#########################################################################
include_directories(${AGENT_INCLUDE_DIRS})

# LINKING LIBRARIES BY DIRECTORY (might generate, e.g., -L/path/to/thing on
# Linux).
###########################################################################
link_directories(${AGENT_LIB_DIRS})

# THE MESOS LIBRARY (generates, e.g., libmesos.so, etc., on Linux).
###################################################################
add_library(${MESOS_TARGET} ${MESOS_SRC})
set_target_properties(
  ${MESOS_TARGET} PROPERTIES
  VERSION ${MESOS_PACKAGE_VERSION}
  SOVERSION ${MESOS_PACKAGE_SOVERSION}
  )
add_dependencies(${MESOS_TARGET} ${AGENT_DEPENDENCIES})

# ADD LINKER FLAGS (generates, e.g., -lglog on Linux).
######################################################
target_link_libraries(${MESOS_TARGET} ${AGENT_LIBS})
