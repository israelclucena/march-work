# march-work
Codes of work during march


require("events").EventEmitter.defaultMaxListeners = 100;

const ENV = { LOCAL: 'local', DEV: 'dev', OW_DEV: 'ONEWEB_DEV', PRE: 'pre' };

/***************** CONFIG *****************/
const MICROFRONTS = {
  globalPosition: ENV.DEV,
  chips: ENV.OW_DEV,
  financialAdvisor: ENV.OW_DEV,
  pfm: ENV.OW_DEV,
  legacy: ENV.PRE,
  mailbx: ENV.PRE,
  globalSearch: ENV.DEV
};
/***************** CONFIG *****************/

/***************** URLS (PRE, DEV, LOCAL ) *****************/
const PARTICULARES_PRE = 'https://particulares.santander.pre.corp';
const ONEWEB_DEV = 'https://oneweb-es.santander.dev.corp';
const PARTICULARES_DEV = 'https://particulares.santander.dev.corp';
const PARTICULARES_LOC = {
  globalPosition: 'http://localhost:4201',
  chips: 'http://localhost:4202',
  financialAdvisor: 'http://localhost:4203',
  pfm: 'http://localhost:4204',
  legacy: 'http://localhost:4205',
  mailbx: 'http://localhost:4206',
  globalSearch: PARTICULARES_DEV
};

const MICROFRONTS_URL = (key) => {
  const urls = {
    [ENV.LOCAL]: PARTICULARES_LOC[key],
    [ENV.DEV]: PARTICULARES_DEV,
    [ENV.OW_DEV]: ONEWEB_DEV,
    [ENV.PRE]: PARTICULARES_PRE
  };
  return urls[MICROFRONTS[key]] || PARTICULARES_DEV;
};
/***************** URLS (PRE, DEV, LOCAL ) *****************/

const microfronts = [
  { id: "mf-ng-00000000-oneweb-global-position", localPath: 'mf/global-position', url: MICROFRONTS_URL('globalPosition') },
  { id: "f-ng-12345678-front-legacy-spain", localPath: 'mf/legacy-spain', url: MICROFRONTS_URL('legacy') },
  { id: "mf-ng-50084805-tracking-asun-cli", url: "https://issues.pru.bsch/tracking/es-ES" },
  { id: "mf-ng-00000000-oneweb-chips", localPath: 'mf/chips', url: MICROFRONTS_URL('chips') },
  { id: "gln-key-saneu-oneweb_eu-finanadvisorui", localPath: 'mf/financialadvisor', url: MICROFRONTS_URL('financialAdvisor') },
  { id: "gln-key-saneu-oneweb_eu-pfmui", localPath: 'mf/financialhealth', url: MICROFRONTS_URL('pfm') },
  { id: "f-ng-50080484-sofret-consulta-contratos", url: "https://inversiones.santander.pre.corp/ccv" },
  { id: "mf-ng-00000000-saneu-mailbx-mfe", localPath: 'mf/mailbox', url: MICROFRONTS_URL('mailbx') },
  { id: "mf-ng-50085254-san-search", localPath: 'mf/sansea', url: MICROFRONTS_URL('globalSearch') },
  { id: "mf-ng-50076635-pss-servicing", url: "https://cuenta-seguros.santander.pre.corp/pss-servicing/es-ES" },
  { id: "mf-ng-50076635-pss", url: "https://cuenta-seguros.santander.pre.corp/pss/es-ES" },
  { id: "san-disnom-nomfront", url: "https://disnom.santander.pre.corp/es-ES" },
  { id: "mf-ng-50078458-homeplanner", url: "https://homeplanner.santander.pre.corp/es-ES" },
  { id: "f-ng-50082389-gdu360-claim-front", url: "https://gdu360.pru.bsch/claim/es-ES/" },
  { id: "mf-ng-50056954-front-decesos-omni", url: "https://seguros-decesos-omni.santander.pre.corp/es-ES" },
  { id: "NOT_REMOVE" },
];

const routes = [
  { context: ["/oneweb/api"], target: `${PARTICULARES_DEV}`, secure: false, changeOrigin: true},
  { context: ["/paas/comdig/static/flame"], target: `${PARTICULARES_PRE}`, secure: false, changeOrigin: true }
];

microfronts.forEach((mf) => {
    let rule = {
      context: [
        `/oneweb/config/${mf.id}`,
        `/oneweb/${mf.id}`
      ],
      target: mf.url,
      secure: false,
      changeOrigin: true,
      onProxyRes: (proxyRes) => {
        // Añadimos caché para agilizar las llamadas de posición global
        if (!mf.url.includes('localhost')) {
          proxyRes.headers['Cache-Control'] = 'public, max-age=360';
        }
      }
    }
    if (!mf.localPath) {
      rule.pathRewrite = {};
      rule.pathRewrite['/oneweb'] = "";
    } else if (mf.url.includes('localhost')) {
      rule.pathRewrite = {};
      rule.pathRewrite['/oneweb/'] = `/oneweb/${mf.localPath}/`;
    }
    console.log(rule)
    routes.push(rule);
});
routes.push({
  context: ['/oneweb/mf/'],
  target: 'https://particulares.santander.pre.corp',
  secure: false,
  changeOrigin: true
});
  
module.exports = routes;
